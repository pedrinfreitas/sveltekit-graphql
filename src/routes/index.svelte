<script context="module" lang="ts">
  import { request, gql } from "graphql-request";

  export interface ICountries {
    countries: ICountry[];
  }
  interface ICountry {
    name: string;
    emoji: string;
  }

  const query = gql`
    {
      countries {
        name
        emoji
      }
    }
  `;

  export const load = async () => {
    const data: ICountries = await request(
      "https://countries.trevorblades.com/",
      query
    );

    return {
      props: {
        data,
      },
    };
  };

  /**
   * USANDO O FETCH DE FORMA NATIVA
   */
  //   export const load = async ({ fetch }) => {
  //     const res = await fetch("https://countries.trevorblades.com/", {
  //       method: "POST",
  //       headers: {
  //         "Content-Type": "application/json",
  //       },
  //       body: JSON.stringify({ query }),
  //     });

  //     const { data } = await res.json();

  //     return {
  //       props: {
  //         data,
  //       },
  //     };
  //   };
</script>

<script lang="ts">
  export let data: ICountries;
</script>

<h1>Countries</h1>

{#each data.countries as country}
  <p>{country.name} - {country.emoji}</p>
{/each}
