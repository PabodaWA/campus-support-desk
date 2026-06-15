# Campus Support Desk (UniHub)

Role-based campus portal UI built with Next.js (App Router) + Tailwind CSS.
This repo currently focuses on the **frontend experience** (sample/demo data) and basic route-level guards.

## 📸 Screenshots

<div align="center">
 <img src=".\src\app\images\UniHub home page.png" alt="Image" style="width: 80%;"/>
 <br>Homepage<br><br>
 <hr>
 <img src=".\src\app\images\Sign In (2).png" alt="Image" style="width: 80%;"/>
 <br>Login<br><br>
 <hr>
 <img src=".\src\app\images\Admin Dashboard (2).png" alt="Image" style="width: 80%;"/>
 <br>Admin Dashboard <br><br>
 <hr>
 <img src=".\src\app\images\Unihub Technician Dashboard.png" alt="Image" style="width: 80%;"/>
 <br>Community Admin Dashboard <br><br>
 <hr>
 <img src=".\src\app\images\Student Dashbord.png" alt="Image" style="width: 80%;"/>
 <br>Student Dashboard <br><br>
 <hr>
 <img src=".\src\app\images\Screenshot 2026-06-16 004518.png" alt="Image" style="width: 80%;"/>
 <hr>
 <img src=".\src\app\images\Screenshot 2026-06-16 004551.png" alt="Image" style="width: 80%;"/>
 <hr>
 <img src=".\src\app\images\Screenshot 2026-06-16 004620.png" alt="Image" style="width: 80%;"/>
 <hr>
</div>

## Requirements

- Node.js 20+ recommended
- npm (comes with Node)

## Getting started (dev)

```bash
npm install
npm run dev
```

Open `http://localhost:3000`.

If port `3000` is busy:

```powershell
$env:PORT=3004; npm run dev
```

## Admin dashboard

Open: `http://localhost:3000/admin`

### Demo mode (recommended for UI testing)

Create a `.env.local` file (it is git-ignored) with:

```bash
NEXT_PUBLIC_DEMO_MODE=true
```

When demo mode is enabled, route guarding is bypassed so you can open role pages directly.

### MongoDB mode (real login/API persistence)

If you want database-backed login and API persistence, use:

```bash
NEXT_PUBLIC_DEMO_MODE=false
MONGODB_URI=mongodb+srv://<username>:<password>@<cluster>/<db>?retryWrites=true&w=majority
MONGODB_DB=campus_support_desk
ADMIN_USERNAME=admin
ADMIN_EMAIL=admin@campus.local
ADMIN_PASSWORD=Admin@12345
```

Then seed an admin user:

```bash
npm run seed:admin
```

`seed:admin` creates or updates an active `ADMIN` account.

### Login (when demo mode is disabled)

If you set `NEXT_PUBLIC_DEMO_MODE=false` (or remove it), role pages are guarded:

1. Open `http://localhost:3000/login`
2. Sign in with your MongoDB-backed user (for seeded admin: `admin` / `Admin@12345` by default)
3. Open `http://localhost:3000/admin`

The app stores a demo session in `localStorage` using:

- `unihub_role`
- `unihub_user`

Guard logic lives in `src/components/auth/RoleGuard.tsx`.

## Useful routes

- `/` landing page
- `/login` demo login (role picker)
- `/admin` admin dashboard
- `/admin/users` user management (demo UI)
- `/admin/faculty` faculty/program structure (demo UI)
- `/admin/groups` grouping (demo UI)
- `/admin/notifications` announcements/notifications (demo UI)
- `/admin/settings` settings (demo UI)
- `/api/health` health endpoint (returns `{ ok: true, ... }`)

## Scripts

- `npm run dev` start dev server
- `npm run seed:admin` create/update MongoDB admin login user
- `npm run build` production build
- `npm run start` start production server (after build)
- `npm run lint` run ESLint

## Scheduled archive job (Vercel)

- `vercel.json` schedules `/api/community-posts/archive` daily at `02:00` UTC.
- Set `CRON_SECRET` in Vercel project environment variables to protect the route.
- The route also accepts `COMMUNITY_CRON_SECRET` for backward compatibility.

## Project structure (high level)

- `src/app` Next.js routes (App Router)
  - `src/app/(app)` role dashboards (admin/student/lecturer/lost-items)
  - `src/app/api` API routes
- `src/components` UI + layout components
- `src/lib` helpers (RBAC, nav config, etc.)
## 👨‍💻 Team Members

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/PabodaWA">
        <img src="https://github.com/PabodaWA.png" width="100px;" alt="Paboda Medhani"/>
        <br />
        <sub><b>Paboda Medhani</b></sub>
      </a>
      <br />
      <sub>Full Stack Developer</sub>
      <br />
      <a href="https://github.com/PabodaWA">GitHub</a>
    </td>
    <td align="center">
      <a href="https://github.com/LakviduUpasara">
        <img src="https://github.com/LakviduUpasara.png" width="100px;" alt="Lakvidu Rathnayake"/>
        <br />
        <sub><b>Lakvidu Rathnayake</b></sub>
      </a>
      <br />
      <sub>Full Stack Developer</sub>
      <br />
      <a href="https://github.com/LakviduUpasara">GitHub</a>
    </td>
    <td align="center">
      <a href="https://github.com/hiruniNwijesinghe">
        <img src="https://github.com/hiruniNwijesinghe.png" width="100px;" alt="Hiruni Wijesinghe"/>
        <br />
        <sub><b>Hiruni Wijesinghe</b></sub>
      </a>
      <br />
      <sub>Full Stack Developer</sub>
      <br />
      <a href="https://github.com/hiruniNwijesinghe">GitHub</a>
    </td>
    <td align="center">
      <a href="https://github.com/SupunKalharaJayasinghe">
        <img src="https://github.com/SupunKalharaJayasinghe.png" width="100px;" alt="Supun Kalhara Jayasinghe"/>
        <br />
        <sub><b>Supun Kalhara Jayasinghe</b></sub>
      </a>
      <br />
      <sub>Full Stack Developer</sub>
      <br />
      <a href="https://github.com/SupunKalharaJayasinghe">GitHub</a>
    </td>
  </tr>
</table>

<p align="center">
  <sub><i>Want to contribute? Check our <a href="#-contributing">Contributing Guidelines</a></i></sub>
</p>

---
## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Code Style Guidelines

- Use ESLint and Prettier configurations provided
- Write meaningful commit messages
- Add comments for complex logic
- Update documentation for new features

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- All contributors who help improve this project

---

Made with ❤️ by the UniHub Team
