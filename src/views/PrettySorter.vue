<template>
    <Sorter sorterNameProp="Pretty Series" imageProp="" />
</template>

<script>
// @ is an alias to /src
import Sorter from '@/components/Sorter.vue'

export default {
  name: 'PrettySorter',
  components: {
    Sorter
  },
  data() {
    return {
      AikatusuDictionaryObject: {
        "Aikatsu": {
          array: [
            {name: "Ichigo Hoshimiya ", image: "https://i.imgur.com/7CpxQ02.png"},
            {name: "Aoi Kiriya ", image: "https://i.imgur.com/3jwdTA5.png"},
            {name: "Ran Shibuki ", image: "https://i.imgur.com/ftgarpY.png"},
            {name: "Otome Arisugawa ", image: "https://i.imgur.com/vgeAsdJ.png"},
            {name: "Yurika Toudou ", image: "https://i.imgur.com/rkeWCwU.png"},
            {name: "Sakura Kitaouji ", image: "https://i.imgur.com/lrwBgd9.png"},
            {name: "Kaede Ichinose ", image: "https://i.imgur.com/TCzc7b9.png"},
            {name: "Mizuki Kanzaki ", image: "https://i.imgur.com/TXRszjk.png"},
            {name: "Seira Otoshiro ", image: "https://i.imgur.com/DTCNzs5.png"},
            {name: "Kii Saegusa ", image: "https://i.imgur.com/2jSgRCi.png"},
            {name: "Sora Kazesawa ", image: "https://i.imgur.com/Lcd117i.png"},
            {name: "Maria Himesato ", image: "https://i.imgur.com/G3gp20K.png"},
            {name: "Mikuru Natsuki ", image: "https://i.imgur.com/JhejxTo.png"},
            {name: "Akari Ozora", image: "https://i.imgur.com/1ORM60h.png"},
            {name: "Hinaki Shinjyo", image: "https://i.imgur.com/Z3aZyyt.png"},
            {name: "Sumire Hikami ", image: "https://i.imgur.com/6lLaDwt.png"},
            {name: "Juri Kurebayashi ", image: "https://i.imgur.com/9hut2jV.png"},
            {name: "Rin Kurosawa ", image: "https://i.imgur.com/Xg94kSp.png"},
            {name: "Madoka Amahane ", image: "https://i.imgur.com/dPBWPhB.png"},
            {name: "Miyabi Fujiwara ", image: "https://i.imgur.com/h1fVTCk.png"},
            {name: "Kokone Kurisu ", image: "https://i.imgur.com/SrrM7q7.png"},
            {name: "Yuu Hattori", image: "https://i.imgur.com/NAs2r36.png"},
            {name: "Shion Kamiya ", image: "https://i.imgur.com/pTjxu9x.png"},
            {name: "Hikari Minowa ", image: "https://i.imgur.com/cEG1wpz.png"},
            {name: "Nono Daichi ", image: "https://i.imgur.com/sIshOGC.png"},
            {name: "Risa Shirakaba ", image: "https://i.imgur.com/vCJk3So.png"},
            {name: "Nina Doujima ", image: "https://i.imgur.com/Eqe4WAT.png"},
            {name: "Noeru Otoshiro ", image: "https://i.imgur.com/4SxxNFr.png"}  
          ]
        },
        "Aikatsu Stars": {
          array: [
            {name: "Yume Nijino", image: "https://i.imgur.com/Npirk1k.png"},
            {name: "Rola Sakuraba", image: "https://i.imgur.com/xlJueB6.png"},
            {name: "Koharu Nanakura", image: "https://i.imgur.com/hz6itFI.png"},
            {name: "Ako Saotome", image: "https://i.imgur.com/Y345Ljp.png"},
            {name: "Hime Shiratori", image: "https://i.imgur.com/5MLFVrJ.png"},
            {name: "Tsubasa Kisaragi", image: "https://i.imgur.com/blxX66E.png"},
            {name: "Yuzu Nikaidou", image: "https://i.imgur.com/Y26ky5U.png"},
            {name: "Yozora Kasumi", image: "https://i.imgur.com/0MNDp0l.png"},
            {name: "Mahiru Kasumi", image: "https://i.imgur.com/lcpttBF.png"},
            {name: "Lily Shirogane", image: "https://i.imgur.com/txdkg6z.png"},
            {name: "Elza Forte", image: "https://i.imgur.com/Tj8V4FC.png"},
            {name: "Kirara Hanazono", image: "https://i.imgur.com/NWKTigv.png"},
            {name: "Rei Kizaki", image: "https://i.imgur.com/gZUyvPu.png"},
            {name: "Aria Futaba", image: "https://i.imgur.com/Iprin4u.png"},
            {name: "Haruka☆Ruka", image: "https://i.imgur.com/foH1KgK.png"} 
          ]
        },
        "Aikatsu Friends": {
          array: [
            {name: "Aine Yūki", image: "https://i.imgur.com/tkUSzG2.png"},
            {name: "Mio Minato", image: "https://i.imgur.com/BPGn66i.png"},
            {name: "Maika Chōno", image: "https://i.imgur.com/Dr0Br3a.png"},
            {name: "Ema Hinata", image: "https://i.imgur.com/bWYWCyL.png"},
            {name: "Karen Kamishiro", image: "https://i.imgur.com/Ij0TE0z.png"},
            {name: "Mirai Asuka", image: "https://i.imgur.com/PZTaXgm.png"},
            {name: "Sakuya Shirayuri", image: "https://i.imgur.com/FDkBeqF.png"},
            {name: "Kaguya Shirayuri", image: "https://i.imgur.com/VGM3g4S.png"},
            {name: "Coco", image: "https://i.imgur.com/BBcq2SS.png"},
            {name: "Marin Manami", image: "https://i.imgur.com/jhPVx6G.png"},
            {name: "Rinna Shinkai", image: "https://i.imgur.com/dshXTDO.png"},
            {name: "Hibiki Tenshō", image: "https://i.imgur.com/rNbyXFw.png"},
            {name: "Alicia Charlotte", image: "https://i.imgur.com/UPJbsPe.png"},
            {name: "Wakaba Harukaze", image: "https://i.imgur.com/Fgi4kLa.png"}
          ]
        },
        "Aikatsu On Parade": {
          array: [
            {name: "Raki Kiseki", image: "https://i.imgur.com/OUCHJyU.png"}
          ]
        },
        "Aikatsu Planet": {
          array: [
            {name: "Hana (Mao Otoha)", image: "https://i.imgur.com/2I7JVnM.png"},
            {name: "Ruli (Ruli Tamaki)", image: "https://i.imgur.com/qqwSc9o.png"},
            {name: "Q-pit (Ayumi Tsukishiro)", image: "https://i.imgur.com/XH5MbsX.png"},
            {name: "Beat (Kyoko Umekoji)", image: "https://i.imgur.com/zIIozKH.png"},
            {name: "Shiori (Shiori Motoya)", image: "https://i.imgur.com/X6H3a4c.png"},
            {name: "Ann (Ann Kurimu)", image: "https://i.imgur.com/ZZF888C.png"},
            {name: "Rose (Meisa Hinata)", image: "https://i.imgur.com/2v0V1zM.png"},
            {name: "Sala (Sala Itoi)", image: "https://i.imgur.com/VUw4suM.png"}
          ]
        },                
      }       
    }
  }

}
</script>
