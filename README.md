<p align="center">
   <a href="https://carbon.ms">
      <img width="auto" height="100" alt="Carbon Logo" src="https://github.com/user-attachments/assets/86a5e583-adac-4bf9-8192-508a0adf2308" />
   </a>
</p>

<p align="center">
    The operating system for manufacturing
    <br />
    <br />
    <a href="https://discord.gg/yGUJWhNqzy">Discord</a>
    ·
    <a href="https://carbon.ms">Website</a>
    ·
    <a href="https://docs.carbon.ms">Documentation</a>
  </p>
</p>
<p align="center">
  <img src="https://img.shields.io/badge/Supabase-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white" alt="Supabase" />
  <img src="https://img.shields.io/badge/Typescript-1a67f3?style=for-the-badge&logo=react&logoColor=white" alt="Typescript" />
  <img src="https://img.shields.io/badge/React-23272F?style=for-the-badge&logo=react&logoColor=white" alt="React" />
</p>

![ERP Screenshot](https://github.com/user-attachments/assets/2e09b891-d5e2-4f68-b924-a1c8ea42d24d)

![MES Screenshot](https://github.com/user-attachments/assets/b04f3644-91aa-4f74-af8d-6f3e12116a6b)

## Does the world need another ERP?

We built Carbon after years of building end-to-end manufacturing systems with off-the-shelf solutions. We realized that:

- Modern, API-first tooling didn't exist
- Vendor lock-in bordered on extortion
- There is no "perfect ERP" because each company is unique

We built Carbon to solve these problems ☝️

## Architecture

Carbon is designed to make it easy for you to extend the platform by building your own apps through our API. We provide some examples to get you started in the [examples](https://github.com/crbnos/carbon/blob/main/examples) folder.

![Carbon Functonality](https://github.com/user-attachments/assets/150c3025-ddcb-4ae4-b7b4-27c670d6cb81)

![Carbon Architecture](https://github.com/user-attachments/assets/3674b2d0-28c7-415f-a8ea-4d8c796337eb)

Features:

- [x] ERP
- [x] MES
- [x] QMS
- [x] Custom Fields
- [x] Nested BoM
- [x] Traceability
- [x] MRP
- [x] Configurator
- [x] MCP Client/Server
- [x] API
- [x] Webhooks
- [ ] Accounting
- [ ] Capacity Planning
- [ ] Simulation
- [ ] [Full Roadmap](https://github.com/orgs/crbnos/projects/1/views/1)

Technical highlights:

- [x] Unified auth and permissions across apps
- [x] Full-stack type safety (Database → UI)
- [x] Realtime database subscriptions
- [x] Attribute-based access control (ABAC)
- [x] Role-based access control (Customer, Supplier, Employee)
- [x] Row-level security (RLS)
- [x] Composable user groups
- [x] Dependency graph for operations
- [x] Third-party integrations

## Techstack

- [React Router](https://reactrouter.com) – framework
- [Typescript](https://www.typescriptlang.org/) – language
- [Tailwind](https://tailwindcss.com) – styling
- [Radix UI](https://radix-ui.com) - behavior
- [Supabase](https://supabase.com) - database
- [Supabase](https://supabase.com) – auth
- [Upstash](https://upstash.com) - cache
- [Trigger](https://trigger.dev) - jobs
- [Resend](https://resend.com) – email
- [Novu](https://novu.co) – notifications
- [Vercel](https://vercel.com) – hosting
- [Stripe](https://stripe.com) - billing

## Codebase

The monorepo follows the Turborepo convention of grouping packages into one of two folders.

1. `/apps` for applications
2. `/packages` for shared code

### `/apps`

| Package Name | Description     | Local Command         |
| ------------ | --------------- | --------------------- |
| `erp`        | ERP Application | `npm run dev`         |
| `mes`        | MES             | `npm run dev:mes`     |
| `academy`    | Academy         | `npm run dev:academy` |
| `starter`    | Starter         | `npm run dev:starter` |

### `/packages`

| Package Name        | Description                                                             |
| ------------------- | ----------------------------------------------------------------------- |
| `@carbon/database`  | Database schema, migrations and types                                   |
| `@carbon/documents` | Transactional PDFs and email templates                                  |
| `@carbon/ee`        | Integration definitions and configurations                              |
| `@carbon/jest`      | Jest preset configuration shared across apps and packages               |
| `@carbon/jobs`      | Background jobs and workers                                             |
| `@carbon/logger`    | Shared logger used across apps                                          |
| `@carbon/react`     | Shared web-based UI components                                          |
| `@carbon/kv`        | Redis cache client                                                      |
| `@carbon/lib`       | Third-party client libraries (slack, resend)                            |
| `@carbon/stripe`    | Stripe integration                                                      |
| `@carbon/tsconfig`  | Shared, extendable tsconfig configuration used across apps and packages |
| `@carbon/utils`     | Shared utility functions used across apps and packages                  |

## Development

### Setup

1. Clone the repo into a public GitHub repository (or fork https://github.com/crbnos/carbon/fork). If want to make the repo private, you should [acquire a commercial license](https://carbon.ms/sales) to comply with the AGPL license.

   ```sh
   git clone https://github.com/crbnos/carbon.git
   ```

2. Go to the project folder

   ```sh
   cd carbon
   ```

Make sure that you have [Docker installed](https://docs.docker.com/desktop/install/mac-install/) on your system since this monorepo uses the Docker for local development.

In addition you must configure the following external services:

| Service     | Purpose                    | URL                                                                    |
| ----------- | -------------------------- | ---------------------------------------------------------------------- |
| Upstash     | Serverless Redis           | [https://console.upstash.com/login](https://console.upstash.com/login) |
| Trigger.dev | Job runner                 | [https://cloud.trigger.dev/login](https://cloud.trigger.dev/login)     |
| Posthog     | Product analytics platform | [https://us.posthog.com/signup](https://us.posthog.com/signup)         |

Each of these services has a free tier which should be plenty to support local development. If you're self hosting, and you don't want to use Upstash or Posthog, it's pretty easy to replace upstash with a redis container in `@carbon/kv` and remove the Posthog analytics.

### Installation

```md
Dựa trên việc kiểm tra mã nguồn của dự án, câu trả lời ngắn gọn là: Hiện tại các dịch vụ này KHÔNG phải là optional (tùy chọn).  
  
Bạn bắt buộc phải cấu hình chúng để dự án có thể khởi động và hoạt động bình thường. Dưới đây là lý do chi tiết:  
  
1. Redis (Upstash) - Bắt buộc  
Dự án sử dụng Redis cho các tác vụ quan trọng như:  
  
Quản lý Session & Permissions: Mỗi khi bạn đăng nhập hoặc thực hiện một hành động, hệ thống sẽ kiểm tra quyền trong Redis.  
Cơ chế bảo vệ: Trong file packages/kv/src/client.ts, mã nguồn có đoạn kiểm tra:  
if (!UPSTASH_REDIS_REST_URL) {  
  throw new Error("UPSTASH_REDIS_REST_URL is not defined");  
}  
Nếu bạn không điền giá trị này vào .env, ứng dụng sẽ dừng ngay lập tức (crash) và báo lỗi.  
2. Trigger.dev (Job Runner) - Bắt buộc cho nghiệp vụ  
Dự án này được thiết kế để xử lý nhiều tác vụ nặng ở chế độ nền (background). Các tính năng cốt lõi sẽ bị lỗi nếu thiếu Trigger.dev:  
  
Xác nhận đơn hàng (Sales Order/Purchase Order).  
Gửi báo giá (Quotes) qua email.  
Cập nhật quyền người dùng hàng loạt.  
Webhooks từ các bên thứ ba (Stripe, Slack). Nếu không có TRIGGER_SECRET_KEY, khi bạn nhấn các nút chức năng này trên giao diện, hệ thống sẽ báo lỗi API vì không thể đẩy tác vụ vào hàng đợi.  
3. Posthog (Analytics) - Có thể coi là Optional (nhưng nên có)  
Đây là dịch vụ theo dõi hành vi người dùng. Nếu bạn bỏ qua, hệ thống có thể vẫn chạy được các tính năng chính, nhưng bạn có thể thấy các lỗi log (console error) ở trình duyệt khi thư viện tracking cố gắng gửi dữ liệu mà không có key.  
  
Lời khuyên cho bạn:  
Sử dụng Free Tier: Cả 3 dịch vụ trên (Upstash, Trigger.dev, Posthog) đều có gói miễn phí rất rộng rãi, đủ để bạn phát triển local mà không tốn xu nào. Bạn chỉ mất khoảng 5 phút để đăng ký và lấy Key.  
Nếu bạn tuyệt đối không muốn dùng Cloud:  
Với Redis: Bạn có thể dựng một container Redis local bằng Docker, nhưng bạn sẽ phải sửa lại code trong packages/kv để chuyển từ dùng @upstash/redis (REST API) sang dùng thư viện ioredis (TCP).  
Với Trigger.dev: Việc thay thế này rất phức tạp vì nó liên quan đến toàn bộ kiến trúc xử lý sự kiện của dự án.  
Kết luận: Cách nhanh nhất để trải nghiệm dự án lúc này là dành ít phút đăng ký tài khoản miễn phí cho các dịch vụ trên và điền vào file .env. Nếu bạn cần hướng dẫn lấy key ở dịch vụ nào, hãy cho tôi biết!
```

First download and initialize the repository dependencies.

```bash
$ nvm use           # use node v20
$ npm install       # install dependencies
$ npm run db:start  # pull and run the containers
```
```
Bước A: Chuẩn bị trên Supabase Cloud  
Bước B: Cấu hình file .env  
Bước C: Đẩy Schema lên Cloud (Migration)  
Vì database trên Cloud của bạn đang trống, bạn cần đẩy cấu trúc bảng của dự án lên đó. Thay vì chạy npm run db:start, bạn làm như sau:  
  
Link dự án:  
npx supabase link --project-ref <your-project-id>  
(Hệ thống sẽ hỏi mật khẩu database bạn đã đặt khi tạo project trên Cloud)  
Push database:  
npx supabase db push  
```

Create an `.env` file and copy the contents of `.env.example` file into it

```bash
$ cp ./.env.example ./.env
```

1. Use the output of `npm run db:start` to set the supabase entries:

- `SUPABASE_SERVICE_ROLE_KEY=[service_role key]`
- `SUPABASE_ANON_KEY=[anon key]`

2. [Create a Redis database in upstash](https://console.upstash.com/redis) and copy the following from the `REST API` section:

- `UPSTASH_REDIS_REST_URL=[UPSTASH_REDIS_REST_URL]`
- `UPSTASH_REDIS_REST_TOKEN=[UPSTASH_REDIS_REST_TOKEN]`

3. Navigate to the project you created in [https://cloud.trigger.dev](https://cloud.trigger.dev) and copy the following from the `Environments & API Keys` section:

- `TRIGGER_SECRET_KEY=[Private 'dev' API Key, starting 'tr_dev_*']`
- `TRIGGER_API_URL="https://api.trigger.dev"`
- `TRIGGER_PROJECT_ID=[Public 'project' key, starting 'proj*]`

4. In Posthog go to [https://[region].posthog.com/project/[project-id]/settings/project-details](https://[region].posthog.com/project/[project-id]/settings/project-details) to find your Project ID and Project API key:

- `POSTHOG_API_HOST=[https://[region].posthog.com]`
- `POSTHOG_PROJECT_PUBLIC_KEY=[Project API Key starting 'phc*']`

5. Add a `STRIPE_SECRET_KEY` from the Stripe admin interface, and then run `npm run -w @carbon/stripe register:stripe` to get a `STRIPE_WEBHOOK_SECRET`

- `STRIPE_SECRET_KEY="sk_test_*************"`
- `STRIPE_WEBHOOK_SECRET="whsec_************"`

6. Signing in requires you to setup one of two methods:
   - Email requires a Resend API key:
     - `RESEND_API_KEY="re_**********"`
     - `RESEND_DOMAIN="carbon.ms"`
   - Sign-in with Google requires a [Google auth client](https://supabase.com/docs/guides/auth/social-login/auth-google) with these variables:
     - `SUPABASE_AUTH_EXTERNAL_GOOGLE_CLIENT_ID="******.apps.googleusercontent.com"`
     - `SUPABASE_AUTH_EXTERNAL_GOOGLE_CLIENT_SECRET="GOCSPX-****************"`
     - `SUPABASE_AUTH_EXTERNAL_GOOGLE_REDIRECT_URI="http://127.0.0.1:54321/auth/v1/callback"`

Then you can run the following:

```bash
$ npm run db:build     # run db migrations and seed script
$ npm run build        # build the packages
```

Finally, start the apps and packages:

```bash
$ npm run dev
$ npm run dev:mes        # npm run dev in all apps & packages
```

After installation you should be able run the apps locally.

| Application     | URL                                                                                                                |
| --------------- | ------------------------------------------------------------------------------------------------------------------ |
| ERP             | [http://localhost:3000](http://localhost:3000)                                                                     |
| MES             | [http://localhost:3001](http://localhost:3001)                                                                     |
| Academy         | [http://localhost:4111](http://localhost:4111)                                                                     |
| Starter         | [http://localhost:4000](http://localhost:4000)                                                                     |
| Postgres        | [postgresql://postgres:postgres@localhost:54322/postgres](postgresql://postgres:postgres@localhost:54322/postgres) |
| Supabase Studio | [http://localhost:54323/project/default](http://localhost:54323/project/default)                                   |
| Mailpit         | [http://localhost:54324](http://localhost:54324)                                                                   |
| Edge Functions  | [http://localhost:54321/functions/v1/<function-name>](http://localhost:54321/functions/v1/<function-name>)         |

### Code Formatting

This project uses [Biome](https://biomejs.dev/) for code formatting and linting. To set up automatic formatting on save in VS Code:

1. Install the [Biome VS Code extension](https://marketplace.visualstudio.com/items?itemName=biomejs.biome)

2. Add the following to your VS Code settings (`.vscode/settings.json` or global settings):

```json
"editor.codeActionsOnSave": {
  "source.organizeImports.biome": "explicit",
  "source.fixAll.biome": "explicit"
},
"editor.defaultFormatter": "biomejs.biome"
```

### Commands

To add an edge function

```bash
$ npm run db:function:new <name>
```

To add a database migration

```bash
$ npm run db:migrate:new <name>
```

To add an AI agent

```bash
$ npm run agent:new <name>
```

To add an AI tool

```bash
$ npm run tool:new <name>
```

To kill the database containers in a non-recoverable way, you can run:

```bash
$ npm run db:kill   # stop and delete all database containers
```

To restart and reseed the database, you can run:

```bash
$ npm run db:build # runs db:kill, db:start, and setup
```

To run a particular application, use the `-w workspace` flag.

For example, to run test command in the `@carbon/react` package you can run:

```
$ npm run test -w @carbon/react
```

To restore a production database locally:

1. Download the production database as a .backup file
2. Rename the `migrations` folder to `_migrations`
3. Restore the database with the following command:

```bash
$ npm run db:build # this should error out at the seed step
$ PGPASSWORD=postgres psql -h localhost -p 54322 -U supabase_admin -d postgres < ~/Downloads/db_cluster-17-11-2025@09-03-36.backup
$ npm run dev
```

4. Rename the `_migraitons` folder back to `migrations`

## API

The API documentation is located in the ERP app at `${ERP}/x/api/js/intro`. It is auto-generated based on changes to the database.

There are two ways to use the API:

1. From another codebase using a supabase client library:

- [Javascript](https://supabase.com/docs/reference/javascript/introduction)
- [Flutter](https://supabase.com/docs/reference/dart/introduction)
- [Python](https://supabase.com/docs/reference/python/introduction)
- [C#](https://supabase.com/docs/reference/csharp/introduction)
- [Swift](https://supabase.com/docs/reference/swift/introduction)
- [Kotlin](https://supabase.com/docs/reference/kotlin/introduction)

2. From within the codebase using our packages.

### From another Codebase

First, set up the necessary credentials in environment variables. For the example below:

1. Navigate to settings in the ERP to generate an API key. Set this in `CARBON_API_KEY`
2. Get the Supabase URL to call (this is `SUPABASE_URL` in your `.env` if hosting locally, e.g. http://localhost:54321). Set this as `CARBON_API_URL`.
3. Get the `SUPABASE_ANON_KEY` e.g. from your .env file. Set this as `CARBON_PUBLIC_KEY`.

If you're self-hosting you can also use the supabase service key instead of the public key for root access. In that case you don't need to include the `carbon-key` header.

```ts
import { Database } from "@carbon/database";
import { createClient } from "@supabase/supabase-js";

const apiKey = process.env.CARBON_API_KEY;
const apiUrl = process.env.CARBON_API_URL;
const publicKey = process.env.CARBON_PUBLIC_KEY;

const carbon = createClient<Database>(apiUrl, publicKey, {
  global: {
    headers: {
      "carbon-key": apiKey,
    },
  },
});

// returns items from the company associated with the api key
const { data, error } = await carbon.from("item").select("*");
```

### From the Monorepo

```tsx
import { getCarbonServiceRole } from "@carbon/auth";
const carbon = getCarbonServiceRole();

// returns all items across companies
const { data, error } = await carbon.from("item").select("*");

// returns items from a specific company
const companyId = "xyz";
const { data, error } = await carbon
  .from("item")
  .select("*")
  .eq("companyId", companyId);
```
