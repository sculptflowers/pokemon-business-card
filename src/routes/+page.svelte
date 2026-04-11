<script lang="ts">
    import BusinessCard from '$lib/BusinessCard.svelte';
    import type { CardData } from '$lib/types';

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

    function handleUpdate(field: keyof CardData, value: string) {
        cardData[field] = value;
    }
</script>
<div class="min-h-screen flex flex-col items-center justify-center p-8">
    <div class="flex-grow flex items-center justify-center">
        <BusinessCard data={cardData} onUpdate={handleUpdate}/>
    </div>
    
    <footer class="mt-8 text-center text-sm text-gray-500 font-display max-w-2xl">
        <p>
            Pokémon and Game Freak are trademarks of Nintendo / Creatures Inc. / GAME FREAK inc.
            This project is fan-made, strictly for educational and non-commercial purposes, and is not affiliated with, endorsed, or sponsored by Nintendo, Creatures Inc., or Game Freak.
        </p>
    </footer>
</div>
