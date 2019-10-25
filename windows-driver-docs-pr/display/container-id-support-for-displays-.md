---
title: ディスプレイ用のコンテナー ID のサポート
description: 表示に対するコンテナー ID のサポートについて説明します。ディスプレイまたはモニターデバイスに埋め込まれているデバイスを視覚的に表現したものです。
ms.assetid: 3149C156-34F4-4C55-AE77-1CC40C2B35BC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 532a5f82f73183cecc9dad4634d99b92a5ba03a2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839807"
---
# <a name="container-id-support-for-displays"></a>ディスプレイ用のコンテナー ID のサポート


このトピックでは、表示のためのコンテナー ID のサポートについて説明します。ディスプレイデバイスまたはモニターデバイスに埋め込まれているデバイスを視覚的に表現したものです。

|                                                                                   |                                          |
|-----------------------------------------------------------------------------------|------------------------------------------|
| Windows Display Driver Model (WDDM) の最小バージョン                               | 1.2                                      |
| Windows の最小バージョン                                                           | 8                                        |
| ドライバーの実装—完全なグラフィックスと表示のみ                              | Mandatory                                |
| [必要条件](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)とテスト |  [モニター コンテナー ID の機能テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/2f657caa-368c-4531-8cec-8faf475125f4) |

 

## <a name="span-idcontainer_id_device_driver_interface__ddi_spanspan-idcontainer_id_device_driver_interface__ddi_spanspan-idcontainer_id_device_driver_interface__ddi_spancontainer-id-device-driver-interface-ddi"></a><span id="Container_ID_device_driver_interface__DDI_"></span><span id="container_id_device_driver_interface__ddi_"></span><span id="CONTAINER_ID_DEVICE_DRIVER_INTERFACE__DDI_"></span>コンテナー ID device driver interface (DDI)


ディスプレイミニポートドライバーで、次の関数と構造を実装します。

-   [*DxgkDdiGetChildContainerId*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_get_child_container_id)
-   [**DXGK\_子\_コンテナー\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_child_container_id)

## <a name="span-idcontainer_id_descriptionspanspan-idcontainer_id_descriptionspanspan-idcontainer_id_descriptionspancontainer-id-description"></a><span id="Container_ID_description"></span><span id="container_id_description"></span><span id="CONTAINER_ID_DESCRIPTION"></span>コンテナー ID の説明


モニタデバイスの新機能により、ユーザーエクスペリエンスが向上します。 特に、ユニバーサルシリアルバス (USB) ハブは、マウスとキーボードを接続するモニター上のよく使用されるコネクタです。 また、HDMI サポートオーディオなどのコネクタと、オーディオスピーカーもモニターに埋め込まれています。 多くの新しいディスプレイデバイスは、タッチ機能をサポートしています。 これにより、ユーザーのデスクトップでネットワークが乱雑になるため、優れたユーザーエクスペリエンスが提供されます。

これらのデバイスの接続と状態を、直感的な方法で視覚的に表現することが重要です。 **[デバイスとプリンター]** ページは、Windows 7 で導入されました。 次に示すように、 **[デバイスとプリンター]** フォルダーには、PC に接続されているインストール済みのデバイスが表示されます。これにより、プリンター、音楽プレーヤー、カメラ、マウス、またはデジタル画像フレームを簡単に確認できます (名前をほんの少しにすることができます)。 同時に、このページでは、同じハードウェア内に含まれているデバイスをグループ化して、ユーザーがすべてのドライバーを簡単に検出できるようにします。

![[デバイスとプリンター] フォルダーの視覚的表現](images/visualdevicesprintersfolder.jpg)

Windows 7 では、デバイスの*コンテナー ID*として、次のような概念が導入されました。 "システムによって提供されるデバイス id 文字列を使用して、コンピューター。 " (「[コンテナー id](https://go.microsoft.com/fwlink/p/?linkid=327784)」を参照してください)。同じコンテナー ID を含むデバイスがグループ化されます。

コンテナー ID の概念を成功させるには、Windows のすべてのデバイスクラスがサポートしている必要があります。また、エコシステム全体でハードウェアを実装する必要があります。 Windows 7 では、オーディオをサポートする複数のモニターが接続されている場合、どのディスプレイがどのオーディオエンドポイントにマップされているかをユーザーが判断するのは簡単ではありません。 タッチデジタイザーにも同じ難易度があります。 Windows 8 では、display device クラスによってコンテナー ID のサポートが追加されます。 これにより、ディスプレイデバイスのすべての機能で同じコンテナー ID を報告し、Windows ユーザーインターフェイスと Api で視覚的に対応させることができます。

## <a name="span-idcontainer_id_user_scenariosspanspan-idcontainer_id_user_scenariosspanspan-idcontainer_id_user_scenariosspancontainer-id-user-scenarios"></a><span id="Container_ID_user_scenarios"></span><span id="container_id_user_scenarios"></span><span id="CONTAINER_ID_USER_SCENARIOS"></span>コンテナー ID のユーザーシナリオ


オーディオスピーカーが埋め込まれているモニターについて、次のワークフローを考えてみましょう。

1.  ユーザーは、HDMI ケーブルを使用してモニターを接続します。
2.  WDDM ドライバーは、Windows グラフィックスタックに表示デバイスの存在を報告します。
3.  Windows グラフィックスタックは、Windows 8 で導入されたデバイスドライバーインターフェイス (DDIs) を使用して、コンテナー ID の WDDM ドライバーを照会します。
4.  ディスプレイドライバーは、このモニターに対してコンテナー ID を照会し、Windows に戻します。
5.  同時に、オーディオドライバーは、完全に同じコンテナー ID を Windows オーディオスタックに渡す必要があります。
6.  **[デバイスとプリンター]** コントロールパネルで表示すると、ディスプレイとスピーカーがグループ化されます。

場合によっては、表示デバイスにコンテナー ID が含まれていないことがあります。 この場合、Windows は、拡張ディスプレイ識別データ (EDID) から取得された製造元 ID、製品 ID、およびシリアル番号を使用して、一意のコンテナー ID を自動的に生成します。 これらの値は一意であるため、コンテナー ID も一意です。 Windows 8 は、同じ情報を WDDM ドライバーに渡し、同じコンテナー ID を生成するためにオーディオドライバーに渡すことができるようにする DDI を提供します。

いくつかのシナリオでは、ディスプレイを運転する所有権は、Windows、WDDM ディスプレイドライバー、ファームウェアの間で切り替えられます。 これらの移行は、リセットまたは再構成されるハードウェアまたはソフトウェアに関連付けられており、画面の点滅やちらつきの原因になる可能性があります。 移行シナリオとその動作については、「 [WDDM 1.2 以降でのシームレスな状態遷移の提供](seamless-state-transitions-in-wddm-1-2-and-later.md)」で説明されています。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定の要件


ハードウェアデバイスがこの機能を実装するときに満たす必要がある要件の詳細については、[モニターコンテナー ID の機能テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/2f657caa-368c-4531-8cec-8faf475125f4)に関する関連する[whck ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)を参照してください。

Windows 8 で追加された機能の確認については、「 [WDDM 1.2 の機能](wddm-v1-2-features.md)」を参照してください。

 

 





