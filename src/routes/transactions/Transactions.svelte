<script>
    import {onDestroy, onMount} from 'svelte';
    // import {recentTxStore} from "../blocks/store.js";
    import RecentTxs from "./RecentTxs.svelte";

    let message;
    let messages = [];
    let aggregates = {};

    // let store;
    let unsubscribe;
    onMount(async () => {
        const store = await import('../blocks/store.js')
        console.log(store.subscribe);

        messages = store.txCache;

        // store.sendMessage(messages);
        unsubscribe = store.recentTxStore.subscribe(currentMessage => {
            if (messages.length > 30)
                messages = [currentMessage, ...messages.slice(0, 30)];
            else
                messages = [currentMessage, ...messages];
        });


        //TODO call unsubscribe
        // onDestroy(unsubscribe);
    })
</script>

<!-- <div class="grid grid-flow-row-dense grid-cols-5 grid-rows-1 gap-x-4">
    <div class=" col-span-3"> -->

        <RecentTxs txs={messages} noOfTxs="10"/>
    <!-- </div>
</div> -->
<style>

</style>
