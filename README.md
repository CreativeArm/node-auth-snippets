# Mongoose Password Hashing (Pre-save Hook)

This repository documents how to securely hash user passwords
using bcrypt and a Mongoose pre-save hook.

## Why this is needed
Passwords should never be stored in plain text.

## Code Example
```js
userSchema.pre("save", async function () {
  if (!this.isModified("password")) return;

  const salt = await bcrypt.genSalt(10);
  this.password = await bcrypt.hash(this.password, salt);
});

# node-auth-snippets
