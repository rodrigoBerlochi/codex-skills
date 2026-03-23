# Framework Selection

Match the stack to the relevant security guidance files in the upstream skill set.

## Backend

- Go backend: `golang-general-backend-security.md`
- Express: `javascript-express-web-server-security.md`
- Next.js server components or backend: `javascript-typescript-nextjs-web-server-security.md`
- Django: `python-django-web-server-security.md`
- FastAPI: `python-fastapi-web-server-security.md`
- Flask: `python-flask-web-server-security.md`

## Frontend

- Generic browser JavaScript frontend: `javascript-general-web-frontend-security.md`
- jQuery frontend: `javascript-jquery-web-frontend-security.md`
- React frontend: `javascript-typescript-react-web-frontend-security.md`
- Vue frontend: `javascript-typescript-vue-web-frontend-security.md`

## Selection Rules

- Load both frontend and backend guidance when the app has both.
- Prefer the most specific framework file available.
- Also apply general secure coding principles when framework-specific guidance is incomplete.
- If the stack is outside these mappings, use established security practice and say that the framework-specific guidance set does not cover it.
