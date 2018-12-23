# docker-compose.yml for Gitlab and GitlabCI

## Installation
1. Start the containers with `docker-compose up`;
2. Create Gitlab database with `docker-compose exec postgresql createdb -U postgres gitlabhq_production`;
3. Open [http://localhost:1080](http://localhost:1080) and set your root password;
4. Log in as a user `root` with the new password;
5. Open [http://localhost:1080/admin/users/new](http://localhost:1080/admin/users/new) and create a new admin user;
6. Edit the new user and set password;
7. Log out and log in as a new user;
8. Update a password if prompted;
9. Open [http://localhost:1080/admin/runners](http://localhost:1080/admin/runners).
10. Copy runner registration token;
11. Execute `docker-compose exec gitlab-runner gitlab-runner register`;
12. When prompted, enter:
  * `http://gitlab:1080` as GitLab coordinator URL;
  * Token obtained at step 10 as gitlab-ci token;
  * Any value as a description;
  * Any tags;
  * `docker` as executor;
  * `ruby:2.3` as default container;
13. Edit `runner/config/config.toml` file;
14. Add `clone_url = "http://gitlab:1080"` in the `[[runners]]` section;
15. Add `network_mode = "gitlab_default"` in the `[runners.docker]` section;
16. Open [http://localhost:1080/admin/runners/1](http://localhost:1080/admin/runners/1);
17. Select `Active`, `Run untagged jobs` checkboxes;
18. Unselect `Protected` and `Lock to current projects` checkboxes.

