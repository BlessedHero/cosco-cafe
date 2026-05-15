# COSCO.kr deployment notes

This project is a static landing page and can be hosted directly on Vercel.

## 1. Deploy the project

From this folder:

```powershell
npx.cmd -y vercel@latest login
npx.cmd -y vercel@latest deploy --prod
```

If the browser login flow fails, create a Vercel token in the Vercel dashboard
and deploy with:

```powershell
npx.cmd -y vercel@latest deploy --prod --token YOUR_VERCEL_TOKEN
```

## 2. Add the custom domain in Vercel

In the Vercel project dashboard, open `Settings > Domains` and add:

- `cosco.kr`
- `www.cosco.kr`

Use Vercel's suggested redirect, usually `cosco.kr` as the primary domain with
`www.cosco.kr` redirecting to it, or the reverse if preferred.

## 3. Add DNS records in Gabia

In Gabia, open `My Gabia > DNS 관리툴 > cosco.kr > 설정 > 레코드 수정`.

Add these records unless Vercel shows different values in the project domain
settings:

| Type | Host | Value |
| --- | --- | --- |
| A | `@` | Use the A record IP shown by Vercel, commonly `76.76.21.21` |
| CNAME | `www` | `cname.vercel-dns-0.com.` |

If Vercel asks for domain ownership verification, also add the exact `TXT`
record it shows. Remove conflicting existing `A`, `AAAA`, or `CNAME` records
for `@` or `www`, then save.

DNS can take minutes to propagate, and Gabia notes it may take up to 48 hours.
