
FROM monitoringState

we want:

entityId
displayname
flag


IF SRE TEAM isnt within the tags as a value,  ( as in, 	tags / key:value,    tags[x where x equals 'SRE Team)
	Then append all tags 



VERTICA TABLE CREATE:

------------------------

CREATE TABLE integration.DYNATRACE_RESTART_REQUIRED (

entity_id VARCHAR(100) PRIMARY KEY,

display_name VARCHAR(255),

restart_required BOOLEAN,

app VARCHAR(100),

app_owner VARCHAR(100),

sre_team VARCHAR(100),

insertion_datetime TIMESTAMP DEFAULT CURRENT_TIMESTAMP

);

  

COMMENT ON TABLE integration.DYNATRACE_RESTART_REQUIRED IS 'Output of dynatrace.cosmote.gr api:

/e/06987e17-dcdb-457b-a19b-4b0a80fd7c3d/api/v1/entity/infrastructure/processes?managementZone=8502848558748003771/e/06987e17-dcdb-457b-a19b-4b0a80fd7c3d/api/v1/entity/infrastructure/processes?managementZone=8502848558748003771/e/06987e17-dcdb-457b-a19b-4b0a80fd7c3d/api/v1/entity/infrastructure/processes?managementZone=8502848558748003771

  

WHERE restartRequired:TRUE';

