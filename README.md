Mern stack developer internship — assessment solutions 

Section 0: Candidate details

- Full name: Annu Parjapati  
- Email address: annuparjapati@59gmail.com
- College / company name: Shanti Institute of Technology (AKTU)  
- GitHub profile URL:  https://github.com/Annuparjapati59/PythonProjects/edit/main/README.md
- Internship batch / group name:B.tech (computer science and engineering)

---

Section 1: Git & GitHub

Difference between Git and GitHub
- Git: Distributed version control system installed locally—tracks changes, branches, merges.  
- GitHub: Cloud platform hosting Git repositories—adds collaboration features like pull requests, issues, CI, and permissions.

Explain git clone, git pull, and git fetch
- git clone: Copies a remote repository to your local machine and sets origin as the default remote.  
- git pull: Fetches remote changes and merges them into your current branch (equivalent to fetch + merge).  
- git fetch: Downloads remote commits/refs without merging—lets you review before integrating.

What is a merge conflict and how do you resolve it?
- Definition: When two commits change the same lines or overlapping areas, Git can’t auto-merge.  
- Resolution:  
  1. Open conflicted files—look for <<<<<<<, =======, >>>>>>>.  
  2. Decide final content—keep one side, combine, or rewrite.  
  3. Mark resolved with git add <file>.  
  4. Complete merge with git commit (or continue rebase with git rebase --continue).

Difference between git merge and git rebase
- Merge: Creates a merge commit—preserves branch history and context; good for shared branches.  
- Rebase: Rewrites commits onto a new base—produces linear history; cleaner logs but must be used carefully (avoid rebasing public branches).

What is .gitignore and why is it important?
- Purpose: Lists files/directories Git should not track (e.g., node_modules, .env, build artifacts).  
- Importance: Keeps repos clean, reduces noise, prevents committing secrets and large binaries.

Assessment repository link
- Repo URL: https:https://github.com/Annuparjapati59/PythonProjects/edit/main/README.md.   
Section 2: MySQL & PostgreSQL

Difference between MySQL and PostgreSQL
- MySQL: Widely used, fast reads, simpler feature set; great for web apps and read-heavy workloads.  
- PostgreSQL: Advanced SQL compliance, strong ACID, rich features (CTEs, window functions, JSONB), extensibility; ideal for complex queries and analytics.

What is a primary key and a foreign key?
- Primary key: Unique identifier for a row—non-null, unique (e.g., id).  
- Foreign key: Column referencing a primary key in another table—enforces relational integrity.

Difference between WHERE and HAVING clause
- WHERE: Filters rows before aggregation—used with base columns.  
- HAVING: Filters groups after aggregation—used with aggregate results (e.g., COUNT, SUM).

Difference between DELETE and TRUNCATE
- DELETE: Removes selected rows; can use WHERE; logged row-by-row; triggers fire; slower for large tables.  
- TRUNCATE: Removes all rows; faster; minimal logging; resets identity; cannot use WHERE; may require higher privileges.

What is database normalization?
- Definition: Structuring tables to reduce redundancy and anomalies.  
- Common forms:  
  - 1NF: Atomic values, no repeating groups.  
  - 2NF: 1NF + no partial dependency on a composite key.  
  - 3NF: 2NF + no transitive dependencies (non-key depends only on key).  
  - BCNF: Stronger form—every determinant is a candidate key.

Explain INNER JOIN, LEFT JOIN, and RIGHT JOIN
- INNER JOIN: Returns rows with matching keys in both tables.  
- LEFT JOIN: Returns all rows from left table + matches from right; unmatched right columns are NULL.  
- RIGHT JOIN: Returns all rows from right table + matches from left; unmatched left columns are NULL.

SQL queries for insert, select, update, delete, and join operations
`sql
-- Schema
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(150) UNIQUE NOT NULL
);

CREATE TABLE orders (
  id SERIAL PRIMARY KEY,
  user_id INT NOT NULL REFERENCES users(id),
  amount DECIMAL(10,2) NOT NULL,
  status VARCHAR(20) NOT NULL,
  created_at TIMESTAMP DEFAULT NOW()
);

-- INSERT
INSERT INTO users (name, email) VALUES ('Annu Parjapati', 'annu@example.com');

-- SELECT
SELECT id, name, email FROM users WHERE email LIKE '%@example.com';

-- UPDATE
UPDATE orders SET status = 'shipped' WHERE id = 42;

-- DELETE
DELETE FROM orders WHERE status = 'cancelled';

-- INNER JOIN: users with their orders
SELECT u.name, o.id AS order_id, o.amount
FROM users u
INNER JOIN orders o ON o.user_id = u.id;

-- LEFT JOIN: all users, with orders if any
SELECT u.name, o.id AS order_id, o.amount
FROM users u
LEFT JOIN orders o ON o.user_id = u.id;

-- Aggregation with HAVING: users with >= 2 orders
SELECT u.id, u.name, COUNT(o.id) AS order_count
FROM users u
LEFT JOIN orders o ON o.user_id = u.id
GROUP BY u.id, u.name
HAVING COUNT(o.id) >= 2;
`

---

Section 3: React fundamentals

What is React and why is it used?
- React: A library for building UI with components and a virtual DOM.  
- Used for: Declarative UI, component reuse, state management, efficient updates, strong ecosystem.

Difference between state and props
- State: Internal, mutable data owned by a component—changes trigger re-render.  
- Props: External, read-only inputs passed from parent—used to configure child components.

What are React hooks?
- Hooks: Functions to use React features in functional components.  
- Core hooks: useState, useEffect, useContext, useReducer, useMemo, useCallback, useRef.

Explain useEffect with an example
- Purpose: Side effects—data fetching, subscriptions, timers, DOM updates.  
- Dependencies:  
  - [] run once on mount,  
  - [a, b] run when a or b changes,  
  - no array runs after every render.
`jsx
import { useEffect, useState } from 'react';

function Users() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    let active = true;
    fetch('/api/users')
      .then(res => res.json())
      .then(data => { if (active) setUsers(data); });
    return () => { active = false; }; // cleanup to avoid setting state after unmount
  }, []); // run once

  return <ul>{users.map(u => <li key={u.id}>{u.name}</li>)}</ul>;
}
`

What is lifting state up?
- Definition: Move shared state to the nearest common ancestor so multiple children can read/update it via props—prevents duplication and keeps a single source of truth.

React practical task link
- Repo URL: https://github.com/<your-username>/<react-task-repo>

---

Section 4: TypeScript basics

What is TypeScript and why is it used?
- TypeScript: A superset of JavaScript adding static types and tooling.  
- Benefits: Early error detection, better IDE support, safer refactors, clearer contracts.

Difference between any and unknown
- any: Opt-out of type checking—can do anything; unsafe.  
- unknown: Type-safe counterpart—must narrow before use; safer for dynamic data.
`ts
let a: any = getValue();
a.trim(); // allowed, may crash at runtime

let u: unknown = getValue();
if (typeof u === 'string') {
  u.trim(); // safe after narrowing
}
`

What are interfaces in TypeScript?
- Interfaces: Named contracts describing object shapes—support extension and declaration merging.
`ts
interface User {
  id: number;
  name: string;
  email?: string; // optional
}

interface Admin extends User {
  role: 'admin';
}
`

What is type inference?
- Definition: TS deduces types from usage—reduces annotations while keeping safety.
`ts
const count = 0;        // inferred as number
const names = ['a'];    // inferred as string[]
const user = { id: 1, name: 'Annu' }; // inferred object shape
`

Explain optional and readonly properties
- Optional (?): Property may be absent—caller not forced to provide it.  
- Readonly: Property cannot be reassigned after initialization—enforces immutability.
`ts
interface Config {
  readonly apiKey: string;
  timeoutMs?: number;
}

const cfg: Config = { apiKey: 'key-123' };
// cfg.apiKey = 'new'; // error


Section 5: General web development

What is a REST API?
- Definition: Architectural style using stateless HTTP, resource-based URLs, and standard methods (GET, POST, PUT, PATCH, DELETE).  
- Principles: Uniform interface, statelessness, cacheable responses, layered system, resource representations (JSON).

Difference between PUT and PATCH
- PUT: Replace the entire resource—idempotent; sending partial data may overwrite missing fields.  
- PATCH: Apply partial updates—non-idempotent by default; only changes specified fields.

What is CORS?
- Definition: Browser security policy controlling cross-origin requests.  
- Mechanism: Preflight (OPTIONS) checks, Access-Control-Allow-* headers; server must explicitly allow origins, methods, and headers.

Difference between SQL and NoSQL databases
- SQL (Relational): Structured schema, ACID transactions, joins; best for complex relationships and consistency.  
- NoSQL: Flexible schemas (document, key-value, column, graph), horizontal scaling; best for high throughput and evolving data models.

Explain MVC architecture
- Model: Data and business logic.  
- View: UI—renders model state.  
- Controller: Handles requests, orchestrates model updates, selects views.  
- Benefit: Separation of concerns—testability, maintainability, parallel development.
  
