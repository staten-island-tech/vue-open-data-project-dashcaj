<script>
const api = "https://data.cityofnewyork.us/resource/hjae-yuav.json"
async function fetchData(api) {
  try {
    const response = await fetch(api);
    const data = await response.json();
    

    console.log(data);
  }
  catch (error) {
    console.log(error);
  }
}

</script>