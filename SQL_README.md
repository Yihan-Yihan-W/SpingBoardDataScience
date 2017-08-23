SQL_Yammer is an exericise using Mode to write SQL queries and generate reports.
https://modeanalytics.com/yihanyihan/reports/5d1898a86885


The SQL queries are following:

SELECT left(date_trunc('week', sub.occurred)::VARCHAR, 10) AS date,
       count (distinct (sub.id)) AS activeusers,
             sub.location AS
location from
  (SELECT users.user_id AS id, events.occurred_at AS occurred, events.location AS
   location
   FROM tutorial.yammer_users users
   JOIN tutorial.yammer_events events
     ON users.user_id = events.user_id
     AND events.event_type = 'engagement'
     AND events.event_name = 'login'
   WHERE extract('year'
                 FROM events.occurred_at) > 2013
     AND users.activated_at IS NOT NULL)sub
GROUP BY sub.location, date
ORDER BY
location


select left(date_trunc('day', created_at)::VARCHAR,10) as date,
count(date_trunc('day', created_at)) as sum_newuser,
count(date_trunc('day', activated_at)) as sum_activate
from tutorial.yammer_users
where (extract('year' from created_at)) >= 2014
group by date
order by date

select 
left(date_trunc('week', sub.occurred)::VARCHAR, 10) as date,
avg(sub.event_age) as "average_event_age",
count(distinct case when sub.active_age > 0 and sub.active_age < 7 then sub.id else null end) as "0 week",
count(distinct case when sub.active_age >= 7 and sub.active_age < 14 then sub.id else null end) as "1 week",
count(distinct case when sub.active_age >= 14 and sub.active_age < 21 then sub.id else null end) as "2 week",
count(distinct case when sub.active_age >= 21 and sub.active_age < 28 then sub.id else null end) as "3 week",
count(distinct case when sub.active_age >= 28 and sub.active_age < 35 then sub.id else null end) as "4 week",
count(distinct case when sub.active_age >= 35 and sub.active_age < 42 then sub.id else null end) as "5 week",
count(distinct case when sub.active_age >= 42 and sub.active_age < 49 then sub.id else null end) as "6 week",
count(distinct case when sub.active_age >= 49 and sub.active_age <56 then sub.id else null end) as "7 week",
count(distinct case when sub.active_age >= 56 and sub.active_age <63 then sub.id else null end) as "8 week",
count(distinct case when sub.active_age >= 63 and sub.active_age < 70 then sub.id else null end) as "9 week",
count(distinct case when sub.active_age >= 70 then sub.id else null end) as "10+ week"
from(
select 
users.user_id as id,
users.created_at as created,
events.occurred_at as occurred,
extract('day' from events.occurred_at - users.created_at) as event_age,
EXTRACT('day' FROM '2014-09-01'::TIMESTAMP - users.activated_at) AS user_age,
EXTRACT('day' FROM '2014-09-01'::TIMESTAMP - users.activated_at) as active_age 
from tutorial.yammer_users users
join tutorial.yammer_events events
on users.user_id = events.user_id
and events.event_type = 'engagement'
and events.event_name = 'login'
where events.occurred_at > '2014-06-01'::TIMESTAMP and users.activated_at IS NOT NULL)sub

group by 1
order by 1

SELECT left(date_trunc('week', occurred_at)::VARCHAR,10) as date,
       COUNT(CASE WHEN action = 'sent_weekly_digest' THEN user_id ELSE NULL END) AS weekly_emails,
       COUNT(CASE WHEN action = 'sent_reengagement_email' THEN user_id ELSE NULL END) AS reengagement_emails,
       COUNT(CASE WHEN action = 'email_open' THEN user_id ELSE NULL END) AS email_opens,
       COUNT(CASE WHEN action = 'email_clickthrough' THEN user_id ELSE NULL END) AS email_clickthroughs
  FROM tutorial.yammer_emails 
 GROUP BY 1
 ORDER BY 1
 
 select 
left(date_trunc('week', sub.occurred)::VARCHAR, 10) as date,
count (distinct (sub.id)) as activeusers,
sub.device_type as device_type
from(
select 
users.user_id as id,
events.occurred_at as occurred,
case when events.device in ('macbook pro','lenovo thinkpad','macbook air','dell inspiron notebook',
          'asus chromebook','dell inspiron desktop','acer aspire notebook','hp pavilion desktop','acer aspire desktop','mac mini')
          THEN 'computer'
     when events.device IN ('iphone 5','samsung galaxy s4','nexus 5','iphone 5s','iphone 4s','nokia lumia 635',
       'htc one','samsung galaxy note','amazon fire phone') THEN 'phone'
    when events.device IN ('ipad air','nexus 7','ipad mini','nexus 10','kindle fire','windows surface',
        'samsumg galaxy tablet') THEN 'tablet' 
    else null end as "device_type"
from tutorial.yammer_users users
join tutorial.yammer_events events
on users.user_id = events.user_id
and events.event_type = 'engagement'
and events.event_name = 'login'
where extract('year' from events.occurred_at) > 2013 and users.activated_at IS NOT NULL)sub

group by sub.device_type, date
order by device_type
