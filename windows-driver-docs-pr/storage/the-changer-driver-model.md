---
title: チェンジャー ドライバー モデル
description: チェンジャー ドライバー モデル
ms.assetid: 87a70ecf-e518-4c22-945b-9056b59fed5a
keywords:
- チェンジャー ドライバー WDK ストレージのアーキテクチャ
- 記憶域チェンジャー ドライバー WDK、アーキテクチャ
- トランスポート要素 WDK チェンジャー
- データ転送の要素の WDK チェンジャー
- storage 要素 WDK チェンジャー
- IEport WDK チェンジャー
- 要素の WDK チェンジャーのインポート/エクスポート
- ドア WDK チェンジャー
- リムーバブル記憶域マネージャーの WDK チェンジャー
- RSM WDK チェンジャー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b004ccdd87364e72805034e2df73b25ea450162
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386814"
---
# <a name="the-changer-driver-model"></a>チェンジャー ドライバー モデル


## <span id="ddk_the_changer_driver_model_kg"></span><span id="DDK_THE_CHANGER_DRIVER_MODEL_KG"></span>


次の図は、チェンジャー ドライバー、ユーザー モード アプリケーションとサービス、大容量記憶装置とポートのドライバー、およびチェンジャー デバイス間の関係を示します。

![チェンジャー ドライバー、ユーザー モード アプリケーションとサービス、大容量記憶装置とポートのドライバー、およびチェンジャー デバイス間のリレーションシップを示す図](images/changer.png)

チェンジャー ドライバー モデル

この図に示すようにユーザー データの転送はチェンジャーのドライブの場合、適切な大容量記憶装置ドライバーによって処理されますスタンドアロン ドライブの場合と同じ Microsoft Win32 要求を使用します。 ただし、大容量記憶装置ドライバーを処理する必要があります、 [ **IOCTL\_ストレージ\_取得\_メディア\_型\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_get_media_types_ex) I/O 要求にはチェンジャーのドライブを制御します。

ユーザー モード サービスを介してユーザー モード アプリケーション アクセス チェンジャー要素には、リムーバブル記憶域マネージャー (RSM) が呼び出されます。 RSM チェンジャー ドライバーの唯一のクライアントは、し、予約、チェンジャーを排他的に使用します。 RSM は、チェンジャー ドライバーにチェンジャーの要素 (たとえば、ドライブにメディアをマウントする場合など) に関連した要求を送信します。 ユーザー モード アプリケーションは、チェンジャー ドライバーに直接要求を送信することはできません。 RSM について詳しくは、Microsoft Windows SDK のドキュメントを参照してください。

チェンジャーの要素は次のとおりです。

-   *トランスポート要素*

    メディア チェンジャー内で他の要素間に移動するロボット コンポーネント。 ほとんどチェンジャーでは、移動されるメディアを保持する 1 つまたは 2 つのいずれかのピッカーを 1 つのトランスポート要素があります。 ハイエンドのフォールト トレラント チェンジャーは、複数のトランスポート要素があります。

-   *要素のデータ転送します。*

    データの読み取りし、書き込みはメディアに元のドライブです。 例では、磁気または光学式ディスク、テープ、CD-ROM または DVD。 通常、チェンジャーには、ドライブの種類 1 つだけにはが含まれています。

-   *Storage 要素*

    ドライブにマウントされていないときに、メディアが格納されるスロット。

チェンジャーは 1 つまたは両方の次の要素にもあります。

-   *インポート/エクスポート*(IEport)

    演算子を挿入する要素または 1 つ以上の削除がすべてではないメディア チェンジャー内で。

-   *ドア*

    一度に 1 つチェンジャー内ですべてのメディアへのアクセスを提供します。 チェンジャーのドアは物理のドアがオペレーターが開いたら、またはすべてのメディアを保持する 1 つの magazine。

チェンジャー miniclass ドライバーがレポートの種類とチェンジャーの要素の数、 [**取得\_チェンジャー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddchgr/ns-ntddchgr-_get_changer_parameters)チェンジャー クラス ドライバーによって要求されたときに構造体します。 具体的には、miniclass ドライバーがアプリケーションがそれらの要素に適切な要求を発行できるように、Ieport と要素の外観に関係なく、これらの定義に従ってドアを報告する必要があります。

 

 




