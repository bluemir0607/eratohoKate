eratohoPM0.995用 Petit Patch-7
主にバグ修正を目的としたパッチです。
ERBフォルダ以下を上書きで導入できます。
Petit Patch無印から6まで全て含みます。
素の本体 or 以前のPetitPatch適応済、どちらに当てても大丈夫です。

GLOBAL番号の変更を含みます。素の本体、または6以前のパッチでの
エンディング記録が正常に引き継がれない場合があります。
（今のところ花嫁ルートのみ）
とりあえず番号一覧添付しました。

修正点：
・花嫁ルート、シスタールートで全能力系エンディングに行き着かない問題の修正
（ENDING\ENDING_4.ERB ENDING_5.ERB 20行目など
　CHECK_LIMITBASEの引数に"美麗", "信仰"を渡していたところを、
　"美麗", "体力"
　に置き換え）
・記録室のエンディング記録が無印で十分に修正されていなかったものの修正
（DATAROOM\DATAROOM.ERB 144行目など
　699を700に　ENDING_2.ERBなど、番号はGLOBAL:700から振っている／
　同154,156,158行目
　数字を1ずつ減らす　page*10+L_LOCALは0-19である／
　同161行目
　PRINTFORM (%GETNAME_PALAM((L_LOCAL+page*10-2)/3)%Lv{3-(L_LOCAL+page*10-2)%3}エンド)
　に置換）
●上記処理後に花嫁ルートだけずれる問題
（ENDING_5.ERB 返すLOCALを全て+1
　他三つが700スタート20枠ずつなので、多数派に合わせる）
・姉妹調教コマンド、処女でない場合INSERTを呼ばないのは妙なので修正
（COM\特殊状況用\COMF902.ERB COMF903.ERB
　処女を見ている条件分岐部分を除去
　　＊実はINSERTの処理、タイミングを考えると@SOURCE_ATHERTRAINに引数つけて、
　　　そっちから呼ぶようにしちゃったほうがいいんではないかともやや思うが今回はこのまま）
　・なんかメッセージの順番が気に食わなかったので同時に修正
　（同ファイル、KOJO_MESSAGE_COMとINSERTの処理を逆順に
　　＊INSERTが複数このタイミングで表示されても奇妙は奇妙だが、
　　　やる前よりはましなのでこのまま。相手が一人ならだいぶ違和感減りそうなので）
・身体で支払うとCALL INSERT, 2, 1と表示される問題
（ARMY.ERB 100行目から
　PRINTFORML
　を外す ただしここの地の文と@INSERTの地の文はあまり親和性がない）

修正していない点・疑問点
・0個売却が可能
　特に支障もなさそうなのでパス
・住み込み時に秘め事を経由するとCFLAG:モードが4でなくなる
（道理で住み込んだはずなのに攫われると思った……）
　どう直すべきか判断つかなかったのでパス
・後宮での中出しによって妊娠した場合金の子しか生まれない
（INSERTを4で呼んでいるため）
　ほかの既存処理とは違う状況なのでどういう結果になるのがいいか悩むのでパス
　なお、他の君主が絡むINSERTでは現在2で処理されている
・野外対面立位でINSERTが呼ばれていない
　単純にINSERT 0,0していいのか悩んだのでパス。
　（分岐を作るかいっそCOMABLEで処女を弾くかetc.）
　

PetitPatch6での修正点：
・姉妹調教コマンドが適正に機能しない問題を修正
（COMABLE.ERB 1426行など
　TARGET != 1
　から
　NO:TARGET != 1
　へ　スター排除／
　SOURCE\SOURCE_ATHERTRAIN.ERB 18行目に
　LOCAL:1 = GETCHARA(2 + COUNT:1)
　を挿入、次行でこれをTARGETに／
　同29,30行目
　1を(LOCAL:10)に置換／
　COM\特殊状況用\COMF902.ERB COMF903.ERB
　2や3を見ている場所を、GETCHARA(2)などで書き換えるように／
　WORK\HITOSARAI.ERB 94行目
　NO:TAG = 99
　を追加　GETCHARAが機能するようにするため）
・花魁称号まわり（PetitPatch4での修正後取得不能な問題）
（CLASS\CLASS.ERB 253行目
　淫妖に／
　同276行目以下
　ARG:1 == 6の場合の特別条件をCOまたは除去　EXP:花魁はリセットされるため
　　花魁訓練の思考力条件があるので問題なかった（見落とし）
・後宮での中出しで主人中出し回数が増えないように
（PREGNANCY\PREGNANCY.ERB 75-76行目
　ARG==4で空分岐を作っておく）

PetitPatch5での修正点：
・魂抜き口上の関数番号ミスを修正(Thx to 175スレ>>178)
（KOJO\MESSAGE.ERB 1114行目から1235行目にかけての
　関数名修正）
・君主影響力0で落ちるバグの修正(Thx to 175スレ>>175)
（ENDING\ENDING_SPECIAL.ERB 185行目
　関数名のほうをあわせました
　姉妹ルート勝利時にこのエンディング出るのは微妙ですが、
　エンディングまわりはまだ整備中だと認識しているので手は入れず）
・コマンド成功時/失敗時の口上が成功率で分岐しない状態の修正
（FUNCTION\FUNCTION.ERB 859行目
　LOCALを渡す／
　同875行目
　(100-LOCAL)を渡す）
・魂抜きで淫妖が上がらない事象の修正
（SOUL\SOUL_SHOP.ERB 311行目に
  GET_ABL = RESULT
　を追加）
・魂が戻ってくるとき何やっても体力経験が引かれる事象の修正
（SOUL\SOUL_SHOP.ERB 335-355行目
　前後入れ替えたうえで、337行目で
　CFLAG:追加魂
　を見るように）
・魂抜きで魔術師の魂入りのとき弓術経験が増えたりする事象の修正
（SOUL\SOUL_SHOP.ERB 271-286行目
　GET_EXPの第二引数に一律+1）
・メイン画面の表示ずれの補正
（SHOP.ERB 413行目&421行目
　PRINTC直後の半角スペース一個とる／
　そのあたり一帯のコマンド文字数＋全角スペースを９文字で揃える）
・服装による姉妹への友好度補正が友好度がありさえすればコマンド問わないバグの修正
（SOURCE\SOURCE_FAVORITE.ERB 137行目
　条件後者をCFLAGからLOSEBASEに）

PetitPatch4での修正点：
・里娘の小袖に着替えたり能力表示で見たりすると落ちる事象の回避
（FUNCTION\CLOTHE_FUNCTION.ERB 123行目
　FORが9までだったのを10までに）
・攫ってきた里娘の称号が正道の姫君Lv0になっているバグの修正
（WORK\HITOSARAI.ERB 157行目
　CFLAG:TAG:称号属性 = 99
　を追加　綿月姉妹も同じ状態ですが違和感ないのでパス）
・花嫁称号、花魁称号を取得しようとすると落ちる不具合の修正
（CLASS\CLASS.ERB 252,253行目
　CASE 6で花魁を返すように。／
　274-275行目を二つ複製。条件の一つを
　ELSEIF ARG:1 == 4 && CFLAG:主人への友好度 < CLASS_MUST_EXP(CHK_HONOR_LV(LOCAL/3))
　に変更／
　その次は冒頭に
　ARG:1 == 6
　を追加、経験の二文字を削る／
　最後の条件冒頭に
　!(ARG:1 == 4 || ARG:1 == 6) &&
　を追加　花魁称号は意図どおりか不明のため要確認）
・エンディング誤字などをちらほら修正
（ENDING\ENDING1.ERB 209行目
　ゴスロリ→花嫁／
　ENDING\ENDING4.ERB 473行目
　RESETCOLOR
　を挿入／
　ENDING\ENDING5.ERB 162行目
　最初の%CALLNAME:TARGET%を%CALLNAME:MASTER%に）
・メイン画面でコマンドが行をまたぐのを修正
（SHOP.ERB 330行以下
　@ENT_PRINTC
　を使うように）
・矯正アイテムが人攫いでうまく働かなくなる事象の修正
（PRINT_SHOP_ITEM.ERB内
　修正場所はERBに記入　量が多くなりすぎた）
　・伴い、陥落がうまく機能しない事象の修正
　（SYSTEM\SYSTEM_TRANSFORM.ERB 141行目
　　TALENT:530を見るように／
　　144行目
　　FLAG:姉妹陥落フラグ |= 1p0
　　を立てるように／
　　150行目,155行目
　　TALENT:554,553を見るように／
　　154行目,159行目
　　CFLAG:対象選択可能をつけるように
　　）
・そんな矯正アイテムが機能しない場合があるのを修正
（SHOP.ERB 33行目で
　TARGETが1から回るように／
　79行目の条件を
　CHARANUM - 1 > TARGET
　に変更
　）
　・付随して、ループ直前に行われていた属性変化のタイミング変更。
　　前ターンの対象以外について処理されるように。
　　（SHOP.ERB 81行目相当にあったものを
　　　78行目に移動、77行目で条件設定）
　・以上の処理でライン入ってないところにDRAWLINE
　　多すぎることがあるのは愛嬌ということで……（手が回らなそうです）
・攫ってきた姉妹の能力値がおかしいバグの修正
（SIMAI_YUUKAI.ERB
　:3:とか:2:とかを:LOCAL:に置き換える
　ここでLOCAL = CHARANUM-1である）
　・さらに普段着着たままのことがあるバグの修正
　（TARGETの一時的な変更をLOCALにするように）
・なんか懐から抜かれてないっぽいぞと思ったので抜かせた
（SIMAI_YUUKAI.ERB 170行目
　MONEY -= LOCAL
　を追加）
　・さらに色が戻ってないのを修正
　（同171行目にRESETCOLOR）

PetitPatch3での修正点：
・戦闘時アイテム使用をキャンセルで落ちるのを修正
（BATTLE\BATTLE_ITEM_USE.ERB 9-10行目
　RESULTが3のとき-1を返すように）
・傾国のローブが行商からいくつも買えるのを修正
（PRINT_SHOP_ITEM.ERB 549行目
　IF ITEM:L_LOCAL
　に書き換え／
　603-605行を複製、片方の条件を
　RESULT == 68 && ITEM:RESULT
　に）

PetitPatch2での修正点：
・普段着売却台詞での死に分岐を生かす
（ITEM.ERB 266行目から
　CFLAG:服装 == 0
　を除去）
・アイテム全部売るが選択不可になる不具合の修正
（ITEM.ERB 316行目の
　ITEM:LOCAL
　→ITEM:BOUGHT
　に修正）
・売るときの店主のコメントが不親切なので直す
（ITEM.ERB 327行目を
　PRINTFORML {LOCAL:1}個ね。全部で${ITEM_COST*LOCAL:1}で引き取るわ
　で置換）
・とりあえず姉妹イベントをラストまで有効化
（OPENING\SIMAI.ERB 355行目で
　FLAG:姉妹イベント=4
　を追加／
　406行目に
　FLAG:姉妹イベント=5
　を追加）
・姉妹イベント第四章ダメージ回復しないでスタートするバグの修正　
（OPENING\SIMAI.ERB 302行目で
　CALL SET_STATUS, 1
　CALL HEALING, 1
　しておく　連戦なので324行目にはとりあえず入れない）
・同じく第四章、依姫と二回戦闘になるバグの修正
（OPENING\SIMAI.ERB 324行目
　第一引数を101に）
・人攫い時の戦闘でもダメージ受けたところから始まるので同様にがんばる
（ELEMENT\ELEMENT_WORK_6.ERB 125,146行目
　↑↑と同様の処理。間はおいてるはずなので回復してていいはず）
・やる気が上がったときに色が戻らないのを戻るように
（EVENT_N.ERB 1565行目に
　RESETCOLOR
　を追加／
　ITEM_USE.ERB 893行目も同様）
・アイテム使用時所持数がおかしかったのを修正
（ITEM_USE.ERB 126行目の
　ITEM:BOUGHT
　→ITEM:LOCAL
　に修正）

PetitPatch無印での修正点：
・着替える対象ではなく現在着ている服のBMI制限が影響するバグの修正
（CLOTHES.ERB 82行目を
　ELSEIF RESULT >= 0 && RESULT != 999 && DITEMTYPE:RESULT:31 >= 1 && CULC_BMI(0) > DITEMTYPE:RESULT:31
　に置換）
　これによって布切れから着替えられないバグからも回復　したはず
・浴衣および純白の薄衣のBMI制限初期設定ミスの修正
（SYSTEM.ERB 23行目および465行目を
　DITEMTYPE:70:31 = 18
　に修正。ついでにコメントの数字が現状とずれていたので修正）
・エンディングリストの能力名が実際とずれているのを修正
（DATAROOM\DATAROOM.ERB 161行目を
　PRINTFORM (%GETNAME_PALAM((L_LOCAL+page*10)/3-1)%Lv{3-(L_LOCAL+page*10)%3})
　に変更）

2014/06/28 望崎