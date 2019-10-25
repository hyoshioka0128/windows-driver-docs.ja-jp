---
Description: このトピックでは、Usbccgp が USB 構成を選択する方法を構成するレジストリ設定に関する情報を提供します。
title: 既定以外の USB 構成を選択するための Usbccgp.sys の構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e2bf07d32a6e04baa14eadab2c365ca65ab6927
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824183"
---
# <a name="configuring-usbccgpsys-to-select-a-non-default-usb-configuration"></a>既定以外の USB 構成を選択するための Usbccgp.sys の構成


このトピックでは、Usbccgp が USB 構成を選択する方法を構成するレジストリ設定に関する情報を提供します。 また、複合デバイスの機能の1つを制御するクライアントドライバーによって送信された選択構成要求を Usbccgp が処理する方法についても説明します。




USB 複合デバイスは、1つの USB デバイス内の複数の関数 (機能デバイス) で構成されます。 Windows が、複合デバイスに対して Microsoft 提供の[USB 汎用親ドライバー](usb-common-class-generic-parent-driver.md) (Usbccgp) を読み込む場合、その時点以降、Usbccgp はデバイスの構成を選択する必要があります。 複合デバイスの各インターフェイスまたはインターフェイスコレクションは、独自の物理デバイスオブジェクト (PDO) を持つ独立したデバイスと同様に、さまざまな点で異なります。 デバイスの構成をリセットすると、クライアントドライバーが制御するものだけでなく、デバイスのすべてのインターフェイスの構成が変更されます。 オペレーティングシステムがこれを許可していません。 したがって、複合デバイスの一連のインターフェイスまたはインターフェイスコレクションを制御するクライアントドライバーは、最初に Usbccgp によって設定される構成を変更することはできません。

ただし、Windows Vista 以降のバージョンの Windows では、次のレジストリ値を追加して、選択する構成を指定できます。

| レジストリ キー               | タスクバーの検索ボックスに       | Value                                                                                                          | 既定値 |
|----------------------------|------------|----------------------------------------------------------------------------------------------------------------|---------------|
| OriginalConfigurationValue | REG\_DWORD | USB 構成インデックス。 Usbccgp は、最初に OriginalConfigurationValue を使用して、選択構成要求を行います。 | 0             |
| AltConfigurationValue      | REG\_DWORD | OriginalConfigurationValue を指定した構成要求が失敗した場合に使用する構成インデックス。      | 0             |

 

既定では、上記のレジストリ設定が存在しない  に**注意**してください。 これらは、USB デバイスの[ハードウェア ("デバイス") キー](https://docs.microsoft.com/windows-hardware/drivers/install/opening-a-device-s-hardware-key)の下に追加する必要があります。

 

このレジストリ設定を使用すると、CCGP ドライバーで別の構成を選択できます。

前の表で説明されているレジストリ値は、USB 定義の構成インデックスに対応しています。これは、構成記述子の**Bconfigurationvalue**メンバー ([**usb\_構成\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_configuration_descriptor)) によって示されます。デバイスの構成記述子で報告される**Bconfigurationnum**の値ではありません。 まず、Usbccgp は、OriginalConfigurationValue で指定された USB 構成インデックスを使用して、親 USB バスドライバー (Usbhub) に選択構成要求を送信します。 要求が失敗した場合、Usbccgp は AlternateConfigurationValue で指定された値を使用しようとします。 AlternateConfigurationValue または OriginalConfigurationValue が無効である場合、Usbccgp は既定値を使用します。

構成の選択要求は、さまざまな理由で失敗する可能性があります。 最も一般的なエラーは、デバイスが要求に対して適切に応答しない場合、または**Bmaxpower**値 (要求された構成で必要な電力) がハブポートでサポートされている電力値を超えた場合に発生します。 たとえば、(OriginalConfigurationValue で指定された) 特定の構成の**Bmaxpower**は 100 milliamperes ですが、ハブポートは 50 milliamperes しか提供できません。 Usbccgp がその構成の選択構成要求を送信すると、USB ドライバースタック (具体的には USB ポートドライバー) が要求に失敗します。 Usbccgp は、AltConfigurationValue で指定された構成を指定することによって、別の選択構成要求を送信します。 代替構成で 50 milliamperes 以下が必要であり、その他の問題が発生しない場合は、選択構成要求が正常に完了します。

### <a href="" id="compatibility-feature"></a>互換性機能

複合デバイスの機能のクライアントドライバーで複合デバイスの構成を選択できない場合でも、クライアントドライバーは Usbccgp に対して選択的な構成要求を送信できます。 要求を作成する方法の詳細については、「 [how To Select a Configuration for a USB Device](how-to-select-a-configuration-for-a-usb-device.md)」を参照してください。 Usbccgp は、クライアントドライバーから選択構成要求を受け取った後、次のタスクを実行します。

1.  は、選択した構成要求を検証するために、USB ポートドライバーによって使用されるのと同じ基準を使用して、受信した要求を検証します。
2.  要求で、現在の設定とは異なるインターフェイスまたはパイプの設定が指定されている場合、Usbccgp は、種類が URB\_関数の URB を送信することによって、選択インターフェイスの要求を発行し\_既存のものを変更するには\_インターフェイスを選択します。新しいインターフェイスとパイプの設定に対する設定。
3.  [**USBD\_インターフェイス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_interface_information)のキャッシュされたコンテンツと[**パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)の構造\_を URB にコピーします。
4.  URB を完了します。

## <a name="related-topics"></a>関連トピック
[USB デバイスの構成を選択する方法](how-to-select-a-configuration-for-a-usb-device.md)  
[USB デバイスの構成](configuring-usb-devices.md)  



