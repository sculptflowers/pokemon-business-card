<script lang="ts">
    import type { CardData } from '$lib/types';
    import BusinessCard from '$lib/BusinessCard.svelte';

    // ── State ($state replaces let + reactive assignments) ───────────────────────
    let cardData: CardData = $state({
        department: '開発部',
        position:   'ゲームディレクター',
        nameJpn:    '大森 滋',
        subName:  'OHMORI SHIGERU',
        company:    '株式会社ゲームフリーク',
        zip:        '154-0004',
        address:    '東京都世田谷区太子堂 4-1-1 キャロットタワー 22F',
        tel:        '+00 0000-0000',
        fax:        '+00 0000-0000',
        email:      'nome@gamefreak.co.jp',
        website:    'http://www.gamefreak.co.jp/',
    });

    let cardRef: HTMLDivElement | undefined = $state();
    let copied: boolean = $state(false);

    // ── Handlers ─────────────────────────────────────────────────────────────────
    function handleUpdate(field: keyof CardData, value: string) {
        cardData[field] = value;
    }

    function copyText() {
        const text = [
            cardData.department,
            cardData.position,
            cardData.nameJpn,
            cardData.subName,
            cardData.company,
            `CEP: ${cardData.zip}`,
            cardData.address,
            `TEL: ${cardData.tel}`,
            `FAX: ${cardData.fax}`,
            `E-Mail: ${cardData.email}`,
            cardData.website,
        ].join('\n');

        navigator.clipboard.writeText(text);
        copied = true;
        setTimeout(() => (copied = false), 2000);
    }

    function printCard() {
        window.print();
    }
</script>

<svelte:head>
    <style>
        @media print {
            body * { visibility: hidden; }
            #card-print, #card-print * { visibility: visible; }
            #card-print {
                position: fixed;
                top: 0; left: 0;
                box-shadow: none !important;
            }
        }
    </style>
</svelte:head>

<main class="min-h-screen bg-gray-100 flex flex-col items-center justify-center gap-6 p-8">

    <h1 class="text-lg font-semibold tracking-wide text-gray-600">
        Editor de Cartão de Visita
    </h1>

    <!-- Card -->
    <div id="card-print" class="shadow-xl">
        <BusinessCard
                data={cardData}
                onUpdate={handleUpdate}
                bind:cardRef
        />
    </div>

    <!-- Actions -->
    <div class="flex gap-3">
        <button
                onclick={copyText}
                class="px-4 py-2 text-sm border border-gray-400 text-gray-600 hover:bg-gray-200 transition-colors rounded"
        >
            {copied ? '✓ Copiado!' : 'Copiar texto'}
        </button>
        <button
                onclick={printCard}
                class="px-4 py-2 text-sm bg-gray-800 text-white hover:bg-gray-600 transition-colors rounded"
        >
            Exportar / Imprimir
        </button>
    </div>

    <p class="text-xs text-gray-400 tracking-widest uppercase">
        Clique em qualquer campo para editar · Enter para confirmar
    </p>

</main>