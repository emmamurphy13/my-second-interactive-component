<!--
@component
This is your page!
-->
<script>
  // Import all the news furniture components
  import ArticleHeader from '$lib/components/ArticleHeader.svelte';
  import ArticleBody from '$lib/components/ArticleBody.svelte';
  import Image from '$lib/components/Image.svelte';
  import GroceryPriceCalculator from '$lib/components/GroceryPriceCalculator.svelte';
  import RelatedLinks from '$lib/components/RelatedLinks.svelte';

  // Article metadata
  let headline = 'Despite Trump\'s Claims, Grocery Prices Are Rising';
  let byline = 'NYCity News Service';
  let pubDate = '2026-01-14';

  // Related stories
  const relatedStories = [
    { headline: 'How America\'s top news organizations escape rigid publishing systems to design beautiful data-driven stories on deadline.', href: 'https://palewi.re/docs/coding-the-news/' },
    { headline: 'How to install, configure and use Visual Studio Code, GitHub and Copilot', href: 'https://palewi.re/docs/coding-the-news/scripts/week-1/' },
    { headline: "How to publish a website with Node.JS and GitHub Actions", href:"https://palewi.re/docs/coding-the-news/scripts/week-2/"},
  ];
</script>

<!-- This sets the page title in the browser tab -->
<svelte:head>
  <title>{headline} | NYCity News Service</title>
  <meta name="description" content="Days away from the first anniversary of President Trump's second term in office, grocery prices are still rising, undercutting his administration's rhetoric about how it is making life more affordable for average Americans." />
</svelte:head>

<!-- Your page content goes here -->
<div class="container">
  
  <!-- Article Header: Headline, byline, and publication date -->
  <ArticleHeader
    {headline}
    {byline}
    {pubDate}
  />

  <!-- Lead Image: Animated gif of students at the journalism school -->
  <Image
    src="/nytfood.webp"
    alt="The Craig Newmark Graduate School of Journalism is at 219 West 40th Street in Midtown Manhattan."
    caption="The Craig Newmark Graduate School of Journalism is at 219 West 40th Street in Midtown Manhattan."
    credit="Craig Newmark Graduate School of Journalism"
  />

  <!-- Article Body: The main story text with proper typography -->
  <ArticleBody>
    <p>
      Days away from the first anniversary of President Trump's second term in office, grocery prices are still rising, undercutting his administration's rhetoric about how it is making life more affordable for average Americans.
    </p>

    <p>
      The price of beef has risen 16.4 percent over the last year. The price of coffee is up a whopping 19.8 percent. The price of lettuce is up 7.3 percent and frozen fish 8.6 percent.
    </p>

    <p>
      Yet Mr. Trump continues to falsely claim otherwise. "Grocery prices are starting to go rapidly down," he said Tuesday afternoon during a speech in Detroit. It's not the first time that he has said food prices are down, even when data show they're not.
    </p>

    <p>
      There is no single reason that food is growing more expensive, and not all food products are pricier. The price of eggs — long a campaign topic — had dropped sharply over the past year. Some of the things that factor into price — fertilizer, machinery, labor and fuel costs, weather, where food is grown and what customers want — are difficult to control. Some of Mr. Trump's actions, like tariffs and immigration crackdowns, have contributed to higher, rather than lower, costs. Low-income families are suffering the most, while middle-class shoppers are starting to take a hit.
    </p>
  </ArticleBody>

  <!-- Interactive Grocery Price Calculator -->
  <GroceryPriceCalculator />

  <!-- Article Body continues -->
  <ArticleBody>
    <p>
      Data released Tuesday by the Bureau of Labor Statistics found the cost of food at home rose 2.4 percent overall in the previous 12 months and 0.7 percent in December alone, the fastest single-month increase since October 2022. That month-over-month gain stood out in an otherwise subdued inflation report.
    </p>

    <p>
      "It's not that panic bells should be ringing or we're seeing the same sort of jump in inflation that we did in 2021 and 2022," said Ricky Volpe, a professor in the agribusiness department at Cal Poly who formerly worked at the Department of Agriculture. "This does, however, hammer home the point that when the current administration claims that grocery prices are down, that is, of course, not correct."
    </p>

    <p>
      Higher prices are particularly affecting low-income consumers, some of whom temporarily lost their SNAP benefits during last year's government shutdown. Those consumers are prioritizing essentials, trading down to cheaper products, buying less and making more frequent trips to the store instead of stocking up, according to grocery executives.
    </p>

    <p>
      "Instead of buying steak, they're buying ground beef and so forth," Susan Morris, the chief executive of Albertsons, said on an earnings call last week. Ronald Sargent, the interim chief executive of Kroger, said last month that consumers were turning to promotions and store brands to save money. And both executives said they were beginning to see similar behavior from middle-income consumers.
    </p>

    <p>
      Not everything is going up; some foods have declined in price. Eggs are 20.9 percent cheaper than a year ago, and the cost of most dairy products has declined modestly. But overall, prices are up in five of the six major food-at-home categories tracked by the Bureau of Labor Statistics.
    </p>

    <p>
      The Trump administration's ever-changing tariff policies have directly affected only a small number of food items in the grocery store, because much of what is consumed in the United States is grown here. But there are some products — like coffee and tropical fruits and vegetables — that are primarily grown abroad and imported into the United States. Many of their prices have climbed on the heels of increased tariffs.
    </p>

    <p>
      The cost of bananas, for instance, was up 5.9 percent in December from year-earlier levels.
    </p>

    <p>
      Consumers are most concerned about price increases in categories like beef, coffee and chocolate. Coffee drinkers are likely to see some relief in the coming months; in November, Mr. Trump removed the 40 percent tariffs on imports from Brazil, a major coffee exporter. But beef eaters likely aren't, as high prices are mostly linked to a half-decade-long drop in the supply of cattle, which will take as long to reverse.
    </p>

    <p>
      In December, ground beef hit a record $6.69 a pound, up from $5.61 a year earlier.
    </p>

    <p>
      Both coffee and beef were rising in price before Mr. Trump took office, highlighting why some consumers may feel that food costs have risen more than the 2.4 percent that the data say they have risen: It's coming on top of years of elevated prices. Grocery store prices are nearly 26 percent higher than they were five years ago, according to the labor bureau.
    </p>

    <p>
      "The headline number, the 2.4 percent increase, in food is not that encouraging, and it's building on already higher numbers," said Michael Swanson, the chief agricultural economist at Wells Fargo Agri-Food Institute. "That is what people really find a challenge."
    </p>

    <p>
      The Agriculture Department expects food-at-home prices to rise 2.3 percent in 2026, about the same as they increased in 2025.
    </p>

    <p>
      Democrats, who were often on the defensive when inflation rose under former President Joseph R. Biden Jr., are seizing on a message of affordability ahead of November's midterm elections. Senator Chuck Schumer of New York, the minority leader, said costs were the No. 1 issue facing American families in an interview Tuesday, with food prices one of the areas Democrats are focused on.
    </p>

    <p>
      Anecdotally, the White House's immigration crackdown has also played a role in driving up food costs. A lack of workers in some areas has led to cherries rotting in Oregon fields, blueberries rotting in New Jersey fields and Pennsylvania dairy farmers selling off cows. But the cost of other fresh fruits, which include berries, has fallen 1.2 percent over the last year, and the price of milk is down 1 percent.
    </p>

    <p>
      Fruit farms and dairies are especially reliant on immigrant labor. Given that those prices have fallen, it isn't clear if the immigration crackdown hasn't yet affected them or if perhaps prices would have decreased more if labor was more readily available.
    </p>

    <p>
      Agriculture groups have warned that they are struggling to find workers, and in November, the Trump administration responded by making it easier for farmers to hire foreign workers.
    </p>

    <p>
      "Labor is clearly the biggest cost driver and makes up about 50 percent of our industry's expenses," said Cathy Burns, the chief executive of the International Fresh Produce Association. She said that limits placed on immigration had made it more difficult for farmers to find workers, and that labor costs in agriculture had been rising for a decade.
    </p>

    <p>
      John David Rainey, the chief financial officer at Walmart, the country's largest grocer, said at a conference last month that he expected "peak impact from the tariff cost to land around the beginning of the first quarter" before subsiding.
    </p>
  </ArticleBody>

  <!-- Related Stories: Links to other articles -->
  <RelatedLinks
    title="Related Stories"
    links={relatedStories}
  />

</div>

<style>
  /* Styles here only apply to this page */
  .container {
    padding: var(--spacing-lg) var(--spacing-md);
    max-width: var(--max-width);
    margin: 0 auto;
  }
</style>
