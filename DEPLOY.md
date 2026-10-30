# Deploying swapsha.com on GitHub Pages

Files in this folder are the whole site. No build step.

## 1. Repo
1. In the SwapSha-com org, create a public repo named `SwapSha-com.github.io`.
2. Push the contents of this folder to `main` (keep `CNAME` and `.nojekyll`).
3. Repo Settings > Pages: Source = Deploy from a branch, `main`, `/ (root)`.

## 2. Verify the domain first (stops anyone else claiming it)
Org Settings > Pages > Add a domain > `swapsha.com`. GitHub shows a TXT record:
- Type TXT, Name `_github-pages-challenge-SwapSha-com`, Value (from GitHub)
Add it at GoDaddy, then click Verify.

## 3. DNS at GoDaddy (Domain > DNS > Manage)
Delete GoDaddy's default parked A record for `@` and any `www` record first.

| Type  | Name | Value                  |
|-------|------|------------------------|
| A     | @    | 185.199.108.153        |
| A     | @    | 185.199.109.153        |
| A     | @    | 185.199.110.153        |
| A     | @    | 185.199.111.153        |
| AAAA  | @    | 2606:50c0:8000::153    |
| AAAA  | @    | 2606:50c0:8001::153    |
| AAAA  | @    | 2606:50c0:8002::153    |
| AAAA  | @    | 2606:50c0:8003::153    |
| CNAME | www  | swapsha-com.github.io  |

Also turn off GoDaddy "Forwarding" for the domain if it is on.

## 4. HTTPS
Repo Settings > Pages: Custom domain = `swapsha.com`. Once the DNS check passes
(minutes to 24 hours), tick "Enforce HTTPS".

## 5. Check
    dig +short swapsha.com A
    dig +short www.swapsha.com CNAME
    curl -I https://swapsha.com

## Email (finchly6819@swapsha.com)
GitHub Pages does not handle mail. Add a forwarding service's MX records at GoDaddy.
Avoid any free plan that publishes your destination inbox in a public TXT record.
