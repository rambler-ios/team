### Образец Appfile

```
for_lane :staging do
  app_identifier 'ru.ramblerco.livejournal'

  apple_id "jenkins.ci@rambler-co.ru"
  team_name 'Rambler Internet Holdings LLC'
  team_id 'UM246WFXVS'
end

for_lane :testing do
  app_identifier 'ru.ramblerco.livejournal'

  apple_id "jenkins.ci@rambler-co.ru"
  team_name 'Rambler Internet Holdings LLC'
  team_id 'UM246WFXVS'
end

for_lane :in_house do
  app_identifier 'ru.ramblerco.livejournal.enterprise'

  apple_id "jenkins.ci@rambler-co.ru"
  team_name 'RAMBLER INTERNET KHOLDING, OOO'
  team_id '7SMPM83ZV6'
end

for_lane :nightly do
  app_identifier 'ru.ramblerco.livejournal.enterprise'

  apple_id "jenkins.ci@rambler-co.ru"
  team_name 'RAMBLER INTERNET KHOLDING, OOO'
  team_id '7SMPM83ZV6'
end
```