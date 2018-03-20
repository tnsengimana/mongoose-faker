# mongoose-faker

`mongoose-faker` is a small library to generate dump data using mongoose models. 

## Installation

`npm install --save mongoose-faker`

## Usage

### Quick usage

```javascript
const faker = require('mongoose-faker');

// Creata a document and save it to the db
const student = await faker.generateObject(StudentModel, { save: true});

// You can also pass in custom fields to your model
const course = await faker.generateObject(CourseModel, {save: true, custom: { students: [ student ] }});
```

### Using sessions

Sometimes you may create lots of data and desire to clean up the db right after you are done. You can use session to accomplish that.

```javascript
const faker = require('mongoose-faker');

describe('Magic', () => {
    before(() => {
        // Tells mongoose-faker that for all objects committed to the db, keep a reference to each one of them.
        faker.newSession();
    });

    after(async () => {
        // Clean up db
        await faker.destroySession();
    });

    it('should pop magic', async () => {
        const student = await faker.generateObject(StudentModel);

        // Pop magic here
    });
})
```

## Credits

Most of the code came from [This repository](https://github.com/thedgmbh/mongoose-dummy). Thanks to [Ahmed Agiza](https://github.com/thedgmbh) for making it available in the first place.
