```SQL
--SQL Query 2
/*Grab the top 1000 players with wins and see how much they spend on items*/
SELECT DISTINCT
count(*) as total_wins, m.player_id as player, SUM(item.price) as cost
FROM
  `pro-tracker-329514.gamecompanydata.matches_info` as m
  JOIN 
  `pro-tracker-329514.gamecompanydata.player_info` as p
  ON 
    m.player_id = p.player_id
  JOIN
  `pro-tracker-329514.gamecompanydata.purchase_info` as pID
  ON 
  p.player_id = pID.player_id
  JOIN 
  `pro-tracker-329514.gamecompanydata.item_info` as item
  ON 
  pID.item_id = item.item_id
    WHERE m.outcome = "win"
    GROUP BY m.player_id
    ORDER BY total_wins DESC
Limit 1000