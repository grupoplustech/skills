---
name: nextjs-secure-actions
description: Security blueprint and audit protocol for Next.js Server Actions. Protects against authorization bypass, IDOR vulnerabilities, parameter pollution, and unvalidated mutations.
version: 1.0.0
metadata:
  category: web
  tags: [nextjs, security, server-actions, react, zod, authentication, idor]
---

# Secure Next.js Server Actions Architecture 🛡️⚡

## ⚠️ The Threat: Server Actions are Public HTTP Endpoints

In Next.js, declaring `'use server'` inside a file exposes that function as a **publicly callable POST endpoint**. Any client can invoke it with arbitrary JSON payloads, bypassing frontend form validations.

---

## 🔒 The Secure Server Action Pattern

```typescript
'use server';

import { z } from 'zod';
import { getServerSession } from 'next-auth'; // Or your auth provider

// 1. Strict Input Schema
const UpdateProfileSchema = z.object({
  userId: z.string().uuid(),
  displayName: z.string().min(2).max(50),
  bio: z.string().max(250).optional(),
});

export type ActionResponse = {
  success: boolean;
  message?: string;
  errors?: Record<string, string[]>;
};

export async function updateProfile(formData: unknown): Promise<ActionResponse> {
  // 2. Authentication Gate
  const session = await getServerSession();
  if (!session?.user) {
    return { success: false, message: 'Unauthorized. Please sign in.' };
  }

  // 3. Schema Validation
  const result = UpdateProfileSchema.safeParse(formData);
  if (!result.success) {
    return { 
      success: false, 
      errors: result.error.flatten().fieldErrors 
    };
  }

  // 4. Authorization / IDOR Check
  if (result.data.userId !== session.user.id) {
    return { success: false, message: 'Forbidden: Cannot modify another user profile.' };
  }

  // 5. Database Mutation
  try {
    // await db.user.update(...)
    return { success: true, message: 'Profile updated successfully.' };
  } catch (error) {
    return { success: false, message: 'Internal server error.' };
  }
}
```
