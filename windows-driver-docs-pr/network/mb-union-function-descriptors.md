---
title: MB 和集合関数記述子
description: このセクションでは、MB デバイス用の共用体関数記述子と MBIM 互換関数について説明します。
ms.assetid: 4B8C63DD-4B8D-40AB-A6DF-0466343E7E45
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc4b35107147fb56cdb82e80f0a519eff4c4c777
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844271"
---
# <a name="mb-union-function-descriptors"></a>MB Union Functional Descriptor


## <a name="union-function-descriptors"></a>共用体関数の記述子


Ufd を実装するモバイルブロードバンドデバイスには、CDC デバイスで必要とされるデバイスクラス/サブクラス/プロトコル 2/0/0 があります。 これにより、Windows によってデバイスに USBCCGP が読み込まれなくなります。 Windows が複合デバイスで USBCCGP を読み込む方法の詳細については、「 [USB 汎用親ドライバー (USBCCGP)](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

Windows による USBCCGP の読み込みを許可するには、デバイスが構成されていないときに、Microsoft OS と互換性のある ID "CDC\_WMC" を報告する必要があります。 互換性のある ID "CDC\_WMC" を検出すると、Windows によって USBCCGP が読み込まれ、USBCCGP によってデバイスの構成が1に設定されます。 USBCCGP は、Microsoft OS 互換 Id に対してもう一度クエリを実行します。 ただし、この時点では、デバイスは Microsoft OS と互換性のある ID "CDC\_WMC" を報告しません。 デバイスは、選択した構成の機能に対して Microsoft OS 互換 Id を報告する場合があります。

![usbhub デバイスが構成されていない場合に microsoft os 記述子のクエリを行う](images/mbim1.png)

USBHUB デバイスが構成されていない場合に Microsoft OS 記述子のクエリを行う

![デバイスは、cdc\-wmc に応答します。これにより、windows は usbccgp を読み込みます。](images/mbim2.png)

デバイスは "CDC\_WMC" で応答します。これにより、Windows は USBCCGP を読み込みます。

![usbccgp は、デバイスの configuration \#1 を選択します。](images/mbim3.png)

USBCCGP は、デバイスの Configuration \#1 を選択します。

![デバイスは構成を選択し、互換性のある id の一覧を morphs します。](images/mbim4.png)

デバイスは構成を選択し、互換性のある Id の一覧を morphs します。 デバイスには、Function2 に必要な CompatID2 が含まれている場合があります。

![読み込みが完了すると、usbccgp は microsoft os 互換 id を再度照会します。](images/mbim5.png)

読み込みが完了すると、USBCCGP は Microsoft OS 互換 Id を再度照会します。

![デバイスは、その機能に対して使用されている互換性のある id を報告します。](images/mbim6.png)

デバイスは、その機能に対して使用されている互換性のある ID を報告します。 USBCCGP は、デバイスの各関数に対して子デバイスノードを作成します。

## <a name="mbim-backward-compatible-functions"></a>MBIM の下位互換性のある関数


NCM 1.0 仕様と下位互換性がある MBIM 関数は、既定で NCM 1.0 関数として機能します。 MBIM 下位互換性のある関数で構成されるモバイルブロードバンドデバイスは、MBIM 関数に対して Microsoft OS 互換 ID "MBIM" を報告する必要があります。 これにより、Windows 8 は NCM 1.0 関数を MBIM 関数として検出し、MBCD を関数ドライバーとして読み込むことができます。

 

 





