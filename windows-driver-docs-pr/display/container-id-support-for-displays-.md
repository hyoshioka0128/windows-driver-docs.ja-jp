---
title: 表示でコンテナー ID のサポート
description: 表示またはモニターのデバイス内に埋め込まれたデバイスのビジュアル表現が表示されます - のコンテナー ID サポートについて説明します。
ms.assetid: 3149C156-34F4-4C55-AE77-1CC40C2B35BC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d613567fd2d9c73ac4fb5388037c5b02db010ff5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532906"
---
# <a name="container-id-support-for-displays"></a>表示でコンテナー ID のサポート


このトピックでは、ディスプレイのコンテナーの ID のサポートを説明します: ディスプレイやモニターのデバイス内に埋め込まれたデバイスのビジュアル表現。

|                                                                                   |                                          |
|-----------------------------------------------------------------------------------|------------------------------------------|
| Windows Display Driver Model (WDDM) の最小バージョン                               | 1.2                                      |
| Windows の最小バージョン                                                           | 8                                        |
| ドライバーの実装: 完全なグラフィックスおよび表示のみ                              | 必須                                |
| [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要件とテスト |  [コンテナー ID のモニターの機能のテスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/2f657caa-368c-4531-8cec-8faf475125f4) |

 

## <a name="span-idcontaineriddevicedriverinterfaceddispanspan-idcontaineriddevicedriverinterfaceddispanspan-idcontaineriddevicedriverinterfaceddispancontainer-id-device-driver-interface-ddi"></a><span id="Container_ID_device_driver_interface__DDI_"></span><span id="container_id_device_driver_interface__ddi_"></span><span id="CONTAINER_ID_DEVICE_DRIVER_INTERFACE__DDI_"></span>コンテナー ID デバイス ドライバー インターフェイス (DDI)


ディスプレイ ミニポート ドライバーでは、この関数と構造体を実装します。

-   [*DxgkDdiGetChildContainerId*](https://msdn.microsoft.com/library/windows/hardware/hh451349)
-   [**DXGK\_子\_コンテナー\_ID**](https://msdn.microsoft.com/library/windows/hardware/hh464005)

## <a name="span-idcontaineriddescriptionspanspan-idcontaineriddescriptionspanspan-idcontaineriddescriptionspancontainer-id-description"></a><span id="Container_ID_description"></span><span id="container_id_description"></span><span id="CONTAINER_ID_DESCRIPTION"></span>コンテナー ID の説明


モニターのデバイスの新しい機能では、優れたユーザー エクスペリエンスを提供できます。 具体的には、ユニバーサル シリアル バス (USB) ハブは人気のコネクタ モニター、マウスとキーボードを接続するためです。 また、HDMI などのコネクタをサポートして、オーディオとオーディオ スピーカーがものモニターに埋め込まれているためです。 新しい表示デバイスの多くは、タッチ機能をサポートします。 これは、ユーザーのデスクトップのワイヤの乱雑さを減らすことで優れたユーザー エクスペリエンスを提供します。

直感的な方法でユーザーに接続し、これらのデバイスの状態を視覚的に表現に重要です。 **デバイスとプリンター**ページは Windows 7 で導入されました。 ここで示すように、**デバイスとプリンター**フォルダーを示しています、ユーザー、PC に接続されているインストールされているデバイス、プリンター、ミュージック プレーヤー、カメラ、マウス、またはデジタル画像 (少しだけ名前) を確認する簡単な方法を提供します。 同時に、このページは、すべてのドライバーを検出するユーザーを容易にできるようにハードウェアの同じ部分内に含まれるこれらのデバイスをグループ化します。

![デバイスとプリンター フォルダーの視覚的表現](images/visualdevicesprintersfolder.jpg)

Windows 7 のマイクロソフトとの概念が導入され、*コンテナー ID*デバイス:"システム提供のデバイスの識別文字列を単一関数または多機能に関連付けられている機能のデバイスを一意にグループ化デバイス、コンピューターにインストールします。" (を参照してください[コンテナー Id](https://go.microsoft.com/fwlink/p/?linkid=327784))。同じコンテナー ID が含まれている場合に、デバイスがグループ化します。

成功すると、コンテナー ID の概念については、Windows のすべてのデバイス クラスをサポートし、エコシステム全体がハードウェアで実装する必要があります。 Windows 7 で、オーディオをサポートする複数のモニターが接続されている場合簡単ではありませんのどのディスプレイにマップするオーディオの終了点を確認します。 同じ問題には、タッチ デジタイザーが存在します。 Windows 8、ディスプレイ デバイスのクラスがコンテナー ID のサポートを追加します。 これにより、同じコンテナー ID を報告し、Windows のユーザー インターフェイスと、Api 取得視覚的にペアになっているディスプレイ デバイスのすべての関数。

## <a name="span-idcontaineriduserscenariosspanspan-idcontaineriduserscenariosspanspan-idcontaineriduserscenariosspancontainer-id-user-scenarios"></a><span id="Container_ID_user_scenarios"></span><span id="container_id_user_scenarios"></span><span id="CONTAINER_ID_USER_SCENARIOS"></span>コンテナー ID のユーザー シナリオ


オーディオ スピーカーが埋め込まれているモニターの次のワークフローを検討してください。

1.  ユーザーは、HDMI ケーブルを使用してモニターを接続します。
2.  WDDM ドライバーでは、Windows グラフィックス スタックをディスプレイ デバイスの存在を報告します。
3.  Windows グラフィックスでは、Windows 8 で導入されたデバイス ドライバー インターフェイス (Ddi) を使用して、コンテナー ID のクエリ WDDM ドライバーをスタックします。
4.  ディスプレイ ドライバーは、コンテナー ID のモニターを照会し、Windows に戻してします。
5.  同時に、オーディオ ドライバーは、Windows オーディオ スタックに正確な同じコンテナー ID を渡す必要があります。
6.  表示する場合、**デバイスとプリンター**コントロール パネル、表示、およびスピーカー グループ化されます。

場合によっては、ディスプレイ デバイスが含まれず、コンテナーの id。 この場合は、Windows は、製造元 ID、製品 ID、およびシリアル番号の取得から、拡張 Display Identification Data (EDID) を使用してコンテナーの一意の ID を自動的に生成します。 これらの値は一意であるため、コンテナー ID も一意にです。 Windows 8 は、同じコンテナー ID を生成するオーディオ ドライバーに渡せるように、WDDM ドライバーに同じ情報を渡す DDI を提供します。

いくつかのシナリオで、ディスプレイを駆動の所有権は、Windows 間で切り替えは、WDDM ドライバーとファームウェアの表示。 これらの遷移は、ハードウェアまたはソフトウェアがリセットまたは再構成し、画面の点滅やちらつきの原因に関連付けられます。 考えられる移行シナリオとその動作は、後ほど[WDDM 1.2 以降のシームレスな状態遷移を提供する](seamless-state-transitions-in-wddm-1-2-and-later.md)します。

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定要件


この機能を実装するときにハードウェア デバイスが満たす必要のある要件については、関連するを参照してください[WHCK ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)で[モニター コンテナー ID の機能テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/2f657caa-368c-4531-8cec-8faf475125f4)します。

参照してください[WDDM 1.2 機能](wddm-v1-2-features.md)に Windows 8 で追加された機能の説明。

 

 





