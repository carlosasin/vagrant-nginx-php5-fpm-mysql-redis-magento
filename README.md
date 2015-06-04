# vagrant-nginx-php5-fpm-mysql-redis-magento
Vagrantfile for Ubuntu + Nginx + PHP5-FPM + Redis + Mysql +Magento + Optional Magento Sample Data


Domain: www.project.local

Project folder: /var/www/project

DB name: project_name

DB user: project_user

DB pass: supersecurepass

Optional magento sample data installation:
Set SAMPLE_DATA=false to disable the sample data installation

## #Fix user magneto admin

Execute this code on the database replacing "firstname", "lastname", "email","username" and "password":

`insert into admin_user
select
(select max(user_id) + 1 from admin_user) user_id,
'Marc' firstname,
'Name' lastname,
'name@domain.com' email,
'admin' username,
MD5('password') password,
now() created,
NULL modified,
NULL logdate,
0 lognum,
0 reload_acl_flag,
1 is_active,
(select max(extra) from admin_user where extra is not null) extra,
NULL,
NULL,
NULL,
NULL,
NULL;`

`insert into admin_role
select
(select max(role_id) + 1 from admin_role) role_id,
(select role_id from admin_role where role_name = 'Administrators') parent_id,
2 tree_level,
0 sort_order,
'U' role_type,
(select user_id from admin_user where username = 'admin') user_id,
'admin' role_name,
0 gws_is_all,
'' gws_websites,
'' gws_store_groups;
`