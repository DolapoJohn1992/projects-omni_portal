Omni-Portal Security Assessment Report
Auditor: Dolapo Adewale John

Date: April 27, 2026

Target: Titan Omni-Portal (Internal Legacy App)

⚙️ Phase 1: Breaking the Gate (SQL Injection)
Vulnerability: SQL Injection (SQLi) Tautology

Payload Used: ' OR 1=1 --

Description: By injecting a SQL tautology into the username field and commenting out the remaining query logic, I successfully bypassed the authentication check without requiring a valid password.

Result: Gained unauthorized access to the application dashboard and unlocked the "View My Orders" functionality.

🧪 Phase 2: Poisoning the Well (Stored XSS)
Vulnerability: Stored Cross-Site Scripting (XSS)

Payload Used: <script>alert(document.cookie)</script>

Captured Session Token: auth_token=[PASTE TOKEN HERE]

Description: I injected a JavaScript payload into the Support Board comment field. Because the application fails to sanitize user input, the script remains stored on the server and executes in the browser of any user viewing the page.

Result: Successfully exfiltrated the auth_token session cookie via a browser alert.

🛠️ Phase 3: Deep Data Mining (API BOLA)
Vulnerability: Broken Object Level Authorization (BOLA)

Target Endpoint: /api/v2/orders/502

Exfiltrated Order ID: 501

Confidential Order Details: * Item: Confidential Server Lease

Dollar Amount: $[PASTE AMOUNT HERE]

Description: After identifying the API structure, I used Burp Suite to perform an Insecure Direct Object Reference (IDOR/BOLA) attack by changing the resource ID in the URL.

Result: Accessed sensitive financial data for an order not associated with my account.

🛡️ Phase 4: Remediation Recommendations
1. SQLi Fix

Recommendation: Utilize Parameterized Queries (Prepared Statements).

Logic: Developers should use placeholders (e.g., ?) for user input rather than concatenating strings. This ensures the database driver treats the input strictly as data, making it impossible for a user to alter the logic of the SQL command.

2. XSS Fix

Recommendation: Implement Context-Aware Output Encoding.

Logic: The application must encode all user-contributed data before it is rendered in the HTML body. Converting characters like < and > into safe HTML entities (like &lt; and &gt;) prevents the browser from executing them as code.

3. API BOLA Fix

Recommendation: Implement Server-Side Authorization Checks.

Logic: The backend must verify that the user identified by the auth_token has the specific right to access the requested resource ID. A check should be performed on every request: if (currentUser.id == order.owner_id).# Omni-Portal Assessment Report
