# states-counties

## Installation

`yarn add states-counties --exact`

## Data Shape

```
{
  state: "CA",
  name: "California",
  counties: [
    {
      msa: 4472,
      pmsa: 8735,
      county: "Ventura",
      state: "CA",
      county_fips: 111,
      state_fips: 6
    }
  ]
}
```

## Usage

### Import Counties for a State

```
import { CA } from 'states-counties'
```

### Import Counties Async (recommended)

This method leverages async module loading and code splitting.
For static data, it's a good alternative to spinning up an endpoint or bundling a large chunk of json.

```
const getCountiesByState = states => {
  const countyLoaders = states.map(state =>
    import(`states-counties/${state.value}`)
      .then(stateData => {
        return {
          label: stateData.default.name,
          options: stateData.default.counties
        };
      })
  );
  return Promise.all(countyLoaders).then(results => results.filter(identity));
};

```

## Source Dataset

https://github.com/hadley/data-counties/blob/master/county-fips.csv
