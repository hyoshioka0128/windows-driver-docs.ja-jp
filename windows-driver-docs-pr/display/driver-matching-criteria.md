---
title: ドライバー一致条件
description: このトピックでは、ドライバーの最適な一致の選択に使用される要素について説明します。
ms.assetid: C41549AE-3FE0-44E8-9D45-1ED1124D010B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e9d1cdf1aa92f3a285cf05c956994011f4953d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570848"
---
# <a name="driver-matching-criteria"></a>ドライバー一致条件


このトピックでは、ドライバーの最適な一致の選択に使用される要素について説明します。

次の要素は、ドライバーの最適な一致の選択に使用されます。 最上位から最下位へ順にそれらのとおりです。

1.  署名
    1.  署名
    2.  符号なし

2.  Scope
    1.  具体的である
    2.  Basic - DNF\_BASIC\_ドライバー

3.  署名のスコア
    1.  内の署名
        1.  \#定義 SIGNERSCORE\_ロゴ\_PREMIUM 0x0D000001
        2.  \#定義 SIGNERSCORE\_ロゴ\_標準 0x0D000002
        3.  \#定義 SIGNERSCORE\_0x0D000003 受信トレイ
        4.  \#SIGNERSCORE 定義\_UNCLASSIFIED 0x0D000004/UNCLASSIFIED/受信トレイを = = 標準を = = PREMIUM = = ときに、SIGNERSCORE\_マスクのフィルタを適用
        5.  \#定義 SIGNERSCORE\_WHQL 0x0D000005//base WHQL します。
        6.  \#定義 SIGNERSCORE\_AUTHENTICODE 0x0F000000

    2.  符号なし内
        1.  \#定義 SIGNERSCORE\_未署名 0x80000000
        2.  \#定義 SIGNERSCORE\_W9X\_0xC0000000 を問題あり
        3.  \#定義 SIGNERSCORE\_不明な 0xFF000000

4.  表示するための特徴のスコア
    1.  Windows 8 WHQL E0
    2.  Windows 8 のプレリリース版ドライバー E3
    3.  Windows 7 WHQL E6
    4.  Windows 7 の受信トレイ EC
    5.  Windows Vista WHQL F6
    6.  Windows Vista の受信トレイ F8
    7.  Microsoft Basic ディスプレイ ドライバー FB
    8.  XDDM サード パーティ FC (Windows 8 では使用されない)
    9.  Windows Vista の障害ドメイン (Windows 8 では使用されません) で XDDM 受信トレイ
    10. VGA FE の (Windows 8 では使用されない)
    11. 既定値またはないスコア FF
    12. 署名されていないドライバー FF
    13. FF にスコア付け機能がありません。

5.  型と一致 (INF の一致が表示されます、モデルのセクションの説明としてインストール セクション、HWID、CompatID を =。 ハードウェア Id が 0 または 1 と 0 個以上の CompatIDs)
    1.  デバイス HardwareID INF HardwareID = =
    2.  デバイス HardwareID INF CompatID = =
    3.  デバイス CompatID INF HardwareID = =
    4.  デバイス CompatID INF CompatID = =

6.  ランクと一致しますデバイスからの一致項目の一覧内の一致の優先順位。
7.  ドライバーの日付
8.  ドライバーのバージョン番号

 

 





