# sql-murder-mystery

A crime has taken place and the detective needs your help. The detective gave you the crime scene report, but you somehow lost it. You vaguely remember that the crime was a murder that occurred sometime on Jan.15, 2018 and that it took place in ​SQL City​. Start by retrieving the corresponding crime scene report from the police department’s database.

        SELECT *
        FROM crime_scene_report
        WHERE type='murder' AND city='SQL City' AND date=20180115;

Security footage shows that there were 2 witnesses. The first witness lives at the last house on "Northwestern Dr". The second witness, named Annabel, lives somewhere on "Franklin Ave".

        SELECT transcript
        FROM person p
        JOIN interview i
        ON p.id=i.person_id
        WHERE name LIKE 'Annabel%'
        AND address_street_name='Franklin Ave'

I saw the murder happen, and I recognized the killer from my gym when I was working out last week on January the 9th.

        SELECT transcript
        FROM person p
        JOIN interview i
        ON p.id=i.person_id
        WHERE address_street_name = 'Northwestern Dr'
        ORDER BY address_number DESC

I heard a gunshot and then saw a man run out. He had a "Get Fit Now Gym" bag. The membership number on the bag started with "48Z". Only gold members have those bags. The man got into a car with a plate that included "H42W".

      SELECT p.name
      FROM person p
      JOIN get_fit_now_member gfnm
      ON p.id=gfnm.person_id
      JOIN drivers_license dl
      ON p.license_id = dl.id
      WHERE gfnm.id LIKE '48Z%'         
      AND dl.plate_number LIKE '%H42W%'

Jeremy Bowers
      
      INSERT INTO solution VALUES (1, 'Jeremy Bowers');
        
        SELECT value FROM solution;

Congrats, you found the murderer! But wait, there's more... If you think you're up for a challenge, try querying the interview transcript of the murderer to find the real villain behind this crime. If you feel especially confident in your SQL skills, try to complete this final step with no more than 2 queries. Use this same INSERT statement with your new suspect to check your answer.

      SELECT transcript
      FROM person p
      JOIN interview i
      ON p.id=i.person_id
      WHERE p.name="Jeremy Bowers"

I was hired by a woman with a lot of money. I don't know her name but I know she's around 5'5" (65") or 5'7" (67"). She has red hair and she drives a Tesla Model S. I know that she attended the SQL Symphony Concert 3 times in December 2017.

      SELECT p.name, COUNT(fb.event_id)
      FROM person p JOIN facebook_event_checkin fb ON p.id=fb.person_id
      JOIN drivers_license dl ON dl.id=p.license_id
      WHERE event_name='SQL Symphony Concert' AND date LIKE '201712%'
      AND hair_color='red' AND car_make='Tesla' AND height BETWEEN 65 AND 67

| name | COUNT(fb.event_id) |
| ----------- | ----------- |
| Miranda Priestly | 3 |

      INSERT INTO solution VALUES (1, 'Miranda Priestly');
        
        SELECT value FROM solution;
        
Congrats, you found the brains behind the murder! Everyone in SQL City hails you as the greatest SQL detective of all time. Time to break out the champagne!
