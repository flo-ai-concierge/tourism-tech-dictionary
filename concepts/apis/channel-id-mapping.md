# Channel ID Mapping

## What it is
Converting numeric codes from an external API into human-readable names for display in your application. APIs often use numbers internally (2018 = Airbnb, 2000 = Direct) because numbers are faster for computers, but humans need readable labels.

## Tourism translation
Like translating reservation source codes into plain labels at the front desk. The booking system stores "CH-2018" internally, but the receptionist sees "Airbnb booking" on their screen. The mapping table is the Rosetta Stone between the computer's language and the staff's language.

## When you'll encounter it
- Displaying booking sources (Airbnb, VRBO, Direct) from a PMS like Hostaway
- Showing message channels in an inbox (SMS, Email, Facebook)
- Any integration where the external system uses codes instead of names

## Related concepts
- Enum — a fixed set of named values in code
- Lookup table — a database table that maps codes to labels
- API documentation — where you find what each code means
