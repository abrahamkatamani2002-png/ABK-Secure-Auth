# Test checklist
| Test | Expected result | Status |
|---|---|---|
| Registration | Auth user created; trigger creates `user` profile | Not run |
| Duplicate registration | Supabase Auth rejects duplicate | Not run |
| Password sign-in | Valid credentials accepted | Not run |
| Email OTP | Correct code verifies; expired/reused code rejected by Auth | Not run |
| Profile read | User sees own profile; admin can view directory | Not run |
| Profile update | User can update own name only | Not run |
| Role escalation | Client cannot update role/status due to column grants and RLS | Not run |
| Admin directory | Normal user denied by RLS | Not run |
| Audit logs | Client cannot insert/update/delete audit rows | Not run |
| Responsive UI | Test 390px, 768px and desktop | Not run |
| Secret scan | No service-role key or DB password in static assets | Not run |
| Backup/recovery | Test managed Supabase backup restore in separate environment | Not run |
