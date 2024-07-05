# InfoShare

SELECT su.user_id,COUNT(pat.pick_user_id) AS 'taskAmount' FROM sys_user su
LEFT JOIN pes_business.pes_aggregate_task pat ON su.user_id = pat.pick_user_id AND pat.status IN (0,1) AND pat.deleted = 0
GROUP BY su.user_id
