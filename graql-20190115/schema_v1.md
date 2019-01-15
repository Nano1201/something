

```
define

    person sub entity,
        has name,
        has expertise_field,
        key email,
        plays Participant,
        plays Employee;

    project sub entity,
        has title,
        has expertise_field,
        has start_date,
        plays Proj;

    organization sub entity,
        has name,
        plays Institute;

    participation sub relationship,
        has post,
        has join_date,
        relates	Proj,
        relates	Participant;

    Study sub relationsip,
        relates Institute,
        relates Employee;

    name sub attribute datatype string;
    expertise_field sub attribute datatype string;
    email sub attribute datatype string;
    title sub attribute datatype string;     ##sub name??
    
    event_date sub attribute datatype date;
    start_date sub event_date;
    join_date sub event_date;
    a
    post sub attribute datatype string regex /[PI, CO_PI, Researcher]/;

```

