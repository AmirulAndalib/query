<script lang="ts">
  import { QueryClient } from '@tanstack/query-core'
  import { createMutation, setQueryClientContext } from '../../src/index.js'
  import { sleep } from '@tanstack/query-test-utils'

  const queryClient = new QueryClient()
  setQueryClientContext(queryClient)

  const mutation = createMutation({
    mutationFn: () =>
      sleep(10).then(() => Promise.reject(new Error('Expected mock error'))),
  })
</script>

<button on:click={() => $mutation.reset()}>Reset</button>
<button on:click={() => $mutation.mutate()}>Mutate</button>

<div>Error: {$mutation.error?.message ?? 'undefined'}</div>
