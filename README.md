# technical-interview-full-stack-dev

Imagine you’re reviewing a teammate’s PR. Please:

1. List any issues you notice (bad practices, security, design, readability, etc.)
2. Suggest improvements based on best practices (DRY, KISS, SOLID, services, testing, etc.)
3. (Optional) Rewrite this function the way you would approach it
4. Describe how you would test this functionality



```
// Controller for creating a user
async function createUser(req, res) {
    const name = req.body.name;
    const email = req.body.email;

    if (!name || !email) {
        return res.status(400).send("Missing data");
    }

    const user = await db.query(`SELECT * FROM users WHERE email = '${email}'`);
    if (user.length > 0) {
        return res.status(409).send("User already exists");
    }

    const created = await db.query(`
        INSERT INTO users (name, email, created_at)
        VALUES ('${name}', '${email}', NOW())
    `);

    // send welcome email
    const msg = `Welcome ${name}!`;
    await mailer.send(email, "Welcome", msg);

    return res.status(201).send("User created");
}
```
