<script lang="ts">
import type { V1DeploymentStatus } from '@kubernetes/client-node';
import Cell from './ui/Cell.svelte';
import Title from './ui/Title.svelte';
import Subtitle from './ui/Subtitle.svelte';
export let artifact: V1DeploymentStatus | undefined;
</script>

{#if artifact}
  <tr>
    <Title>Status</Title>
  </tr>
  <tr>
    <Cell>Replicas</Cell>
    <Cell>
      Desired: {artifact.replicas ?? 'N/A'}, Updated: {artifact.updatedReplicas ?? 'N/A'}, Total: {artifact.replicas ??
        'N/A'}, Available: {artifact.availableReplicas ?? 'N/A'}, Unavailable: {artifact.unavailableReplicas ?? 'N/A'}
    </Cell>
  </tr>
  {#if artifact.conditions}
    <tr>
      <Title>Conditions</Title>
    </tr>
    {#each artifact.conditions as condition}
      <tr>
        <Subtitle>{condition.reason}</Subtitle>
      </tr>
      <tr>
        <Cell>Type</Cell>
        <Cell>{condition.type}</Cell>
      </tr>
      <tr>
        <Cell>Status</Cell>
        <Cell>{condition.status}</Cell>
      </tr>
      <tr>
        <Cell>Reason</Cell>
        <Cell>{condition.reason}</Cell>
      </tr>
      <tr>
        <Cell>Message</Cell>
        <Cell>{condition.message}</Cell>
      </tr>
    {/each}
  {/if}
{/if}
