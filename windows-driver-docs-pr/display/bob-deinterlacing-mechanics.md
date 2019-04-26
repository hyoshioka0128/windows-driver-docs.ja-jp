---
title: bob デインターレース メカニズム
description: bob デインターレース メカニズム
ms.assetid: 1735f9c6-ac83-4a6a-bc6f-4d4a193876dd
keywords:
- WDK の DirectX va なので、mechanics デインター レースを bob します。
- WDK DirectX VA のフィールドをインターリーブ
- stride WDK DirectX VA
- WDK DirectX va なので、bob、mechanics デインター レース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afedf91ae8d5627c2bb96dd6d6a9998888f2dd71
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358200"
---
# <a name="bob-deinterlacing-mechanics"></a>bob デインターレース メカニズム


## <span id="ddk_bob_deinterlacing_mechanics_gg"></span><span id="DDK_BOB_DEINTERLACING_MECHANICS_GG"></span>


単純な bob スタイル デインター レース ビット ブロック転送を実行できるすべてのグラフィックス アダプターを実行できます。 サーフェスにインターリーブの 2 つのフィールドが含まれている場合、各フィールドを分離する、画面のメモリ レイアウトを解釈できます。 これは、元のサーフェスのストライドを 2 倍と、画面の半分の高さを分割することで実現されます。 この方法では、2 つのフィールドが分離され後、は、個々 のフィールドに適切なフレームの高さを拡大して deinterlaced ことができます。

あるビデオ画像のピクセルの縦横比を修正するのには、追加の水平方向の拡大または縮小も適用できます。 ディスプレイ ドライバーは、これを行う DirectX ビデオ ミキシング レンダラー (VMR) する機能を確認できます。 個々 のフィールドの高さは、行のレプリケーションか、可能であれば、フィルター選択された stretch 垂直方向に拡大できます。 行のレプリケーションの方法を使用する場合、結果のイメージはむらを持ちます。 フィルター選択された伸縮を使用すると、結果のイメージがぼやけて外観にあります。

次の図は、インターリーブの 2 つのフィールドを含むビデオの画面を示します。

![インターリーブの 2 つのフィールドを格納している画面のメモリ レイアウトを示す図](images/deinterlace.png)

指定されたビデオのサンプルには、インターリーブされた 2 つのフィールドが含まれている場合、 **DXVA\_SampleFieldInterleavedEvenFirst**と**DXVA\_SampleFieldInterleavedOddFirst**メンバー、 [ **DXVA\_SampleFormat** ](https://msdn.microsoft.com/library/windows/hardware/ff564045)列挙型、2 番目のフィールドの開始時刻を使用して計算、 **rtStart**と**rtEnd**のメンバー、 [ **DXVA\_VideoSample** ](https://msdn.microsoft.com/library/windows/hardware/ff564085)次のように構造体します。

(**rtStart** + **rtEnd**)/2

最初のフィールドの終了時刻は、2 番目のフィールドの開始時刻です。

 

 





