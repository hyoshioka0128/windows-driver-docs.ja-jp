---
title: MB の統合機能ディスクリプター
description: このセクションでは、統合機能ディスクリプター、MBIM 下位互換性のある関数 MB デバイスについて説明します。
ms.assetid: 4B8C63DD-4B8D-40AB-A6DF-0466343E7E45
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aeb663a4eacb06832dcca998838a85d770651b38
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374036"
---
# <a name="mb-union-function-descriptors"></a>MB Union Functional Descriptor


## <a name="union-function-descriptors"></a>統合機能ディスクリプター


Ufd を実装しているモバイル ブロード バンド デバイスはデバイス クラスを持つ/サブクラス プロトコル/2 の/0]、[CDC のデバイスに必要な 0 として。 これは Windows がデバイスで USBCCGP を読み込みすることを防ぎます。 Windows が複合デバイスで USBCCGP を読み込む方法については、次を参照してください。 [USB 汎用親ドライバー (Usbccgp.sys)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

Microsoft OS 互換性 ID を報告する Windows USBCCGP を読み込むには、デバイスに必要な"CDC\_WMC"デバイスが構成されていない場合。 互換性のある ID を検出した後は"CDC\_WMC"、USBCCGP と USBCCGP の Windows が読み込まれ、デバイス 1 に、構成を設定します。 USBCCGP は Microsoft OS の互換性のある id し、もう一度照会します。 今回は、ただし、する必要がありますを報告しないデバイスの Microsoft OS 互換性 ID"CDC\_WMC"。 デバイスによって、選択した構成内の関数の Microsoft OS 互換性 Id を報告する必要があります。

![microsoft os ディスクリプター、デバイスが構成されていない場合の usbhub クエリ](images/mbim1.png)

デバイスが構成されていない場合は、Microsoft OS 記述子の USBHUB クエリ

![デバイスは、cdc は応答\-wmc が windows usbccgp を読み込めません。](images/mbim2.png)

デバイスが応答で"CDC\_WMC"、それが原因で Windows を読み込む USBCCGP

![usbccgp 構成を選択します。\#デバイス上の 1。](images/mbim3.png)

USBCCGP 構成を選択します。\#デバイス上の 1。

![デバイスは、構成を選択し、互換性 id の一覧のモーフィングを行います。](images/mbim4.png)

デバイスは、構成を選択し、互換性 Id の一覧のモーフィングを行います。 デバイスは、Function2 に必要な CompatID2 を含めることができます。

![読み込み後、usbccgp microsoft os 互換性 id 再び照会します。](images/mbim5.png)

後の読み込み、もう一度 Microsoft OS の互換性のある id USBCCGP クエリ。

![デバイスは、その関数に対して持っている任意の互換性のある id を報告します。](images/mbim6.png)

デバイスは、その関数に対して持っている任意の互換性のある ID を報告します。 USBCCGP し、子ノードを作成デバイス関数ごとに、デバイスにします。

## <a name="mbim-backward-compatible-functions"></a>MBIM 下位互換性のある関数


NCM 1.0 仕様の旧バージョンとの互換性のある MBIM 関数は、既定 NCM 1.0 関数として提供されます。 MBIM 下位互換性のある関数で構成されているモバイル ブロード バンド デバイスは、MBIM 関数の"MBIM"の Microsoft OS 互換性 ID を報告する必要があります。 これにより、Windows 8 を MBIM 関数として NCM 1.0 関数を検出し、関数のドライバーとして MBCD をロードできます。

 

 





