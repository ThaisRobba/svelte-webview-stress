<script>
  import Heading from '../components/Heading.svelte'
  import TransactionItem from '../components/TransactionItem.svelte'

  const rand = () => Math.random() > 0.5


  const createTransaction = () => {
    return {
      name: rand() ? 'joão silva' : 'beatriz gomez',
      amount: rand() ? 'R$ 1.400,00' : 'R$ 223,87',
      date: new Date().toISOString(),
      status: rand() ? 'Em análise' : 'Aprovado',
    }
  }

  const mockTransactions = Array.from({ length: 10000 }, createTransaction)

  let filter = ''

  $: transactions = mockTransactions.filter((x) => filter === '' || x.name.includes(filter))
</script>

<div>
    <div class="header">
        <Heading text="Minhas vendas" />
        <input
          class="search"
          type="search"
          id="site-search"
          name="search"
          bind:value={filter}
        />
    </div>
    {#each transactions as transaction}
      <TransactionItem {...transaction} />
    {/each}
</div>

<style>
  .header {
    padding: 24px 16px;
    background-color: #F2F2F3;
    display: flex;
  }

  input {
    flex-grow: 2;
    margin-left: 16px;
    padding: 6px;
    border: none;
  }
</style>