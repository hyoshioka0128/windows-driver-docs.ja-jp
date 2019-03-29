---
Description: This topic provides information about registry settings that configure the way Usbccgp.sys selects a USB configuration.
title: 既定以外の USB 構成を選択するための Usbccgp.sys の構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45009bca190ff1fc97611511e6282af18781436a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581276"
---
# <a name="configuring-usbccgpsys-to-select-a-non-default-usb-configuration"></a>既定以外の USB 構成を選択するための Usbccgp.sys の構成


このトピックで、Usbccgp.sys USB 構成を選択する方法を構成するレジストリ設定について説明します。 Usbccgp.sys が複合デバイスの機能のいずれかを制御するクライアント ドライバーによって送信された選択構成要求を処理する方法についても説明します。




複合 USB デバイスは、1 つの USB デバイス内の複数の関数 (デバイスの機能) で構成されます。 Windows が Microsoft から提供されたを読み込む場合[汎用的な親の USB ドライバー](usb-common-class-generic-parent-driver.md) (Usbccgp.sys) 複合デバイスは、転送、その時点からで、Usbccgp.sys 担当、デバイスの構成を選択します。 それぞれのインターフェイスまたは複合デバイスのインターフェイスのコレクションは、独自の物理デバイス オブジェクト (PDO) を持つ別のデバイスなど、多くの点では。 デバイスの構成をリセットするだけでなく、1 つのクライアント ドライバーを制御するデバイスのインターフェイスのすべての設定を変更します。 オペレーティング システムで、これが許可されません。 そのため、一連のインターフェイスまたは複合デバイスのインターフェイスのコレクションを制御するクライアント ドライバーで、Usbccgp.sys で最初に設定されている構成を変更できません。

ただし、Windows Vista および以降のバージョンの Windows では、選択する構成を指定する次のレジストリ値を追加できます。

| レジストリ キー               | 型       | 値                                                                                                          | 既定値 |
|----------------------------|------------|----------------------------------------------------------------------------------------------------------------|---------------|
| OriginalConfigurationValue | REG\_DWORD | USB の構成のインデックス。 Usbccgp.sys は、まず、OriginalConfigurationValue を選択構成要求を使用します。 | 0             |
| AltConfigurationValue      | REG\_DWORD | OriginalConfigurationValue と選択構成要求が失敗した場合に使用する構成のインデックス。      | 0             |

 

**注**  上記のレジストリ設定が既定で存在しません。 これらは、下に追加する必要があります、 [(「デバイス」とも呼ばれます) のハードウェア キー](https://docs.microsoft.com/windows-hardware/drivers/install/opening-a-device-s-hardware-key)の USB デバイスです。

 

レジストリ設定は、代替の構成を選択する CCGP ドライバーを使用できます。

レジストリ値を前の表で説明されているインデックスに対応する、USB で定義された構成で示される、 **bConfigurationValue**構成記述子のメンバー ([**USB\_構成\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff539241)) と*いない*によって、 **bConfigurationNum**デバイスの構成で報告される値記述子。 最初で、Usbccgp.sys は、OriginalConfigurationValue で指定された USB 構成のインデックスを使用して親 USB バス ドライバー (Usbhub.sys) を選択構成要求を送信します。 要求が失敗している場合で、Usbccgp.sys AlternateConfigurationValue で指定された値を使用しようとします。 Usbccgp.sys では、AlternateConfigurationValue または OriginalConfigurationValue が有効でない場合、既定値が使用されます。

選択構成要求は、多くの理由で失敗します。 最も一般的なエラーは、または要求にデバイスが適切に応答しないときに発生します。、 **bMaxPower**値 (要求された構成に必要な電力) は、ハブのポートでサポートされている power 値を超えています。 たとえば、 **bMaxPower** (OriginalConfigurationValue で指定された) 特定の構成は 100 ミリアンペアいますが、ハブのポートは 50 ミリアンペアを提供することのみです。 USB ドライバー スタック (具体的には、USB ポート ドライバー) で、Usbccgp.sys では、その構成の選択構成要求を送信するときに、要求は失敗します。 次で、Usbccgp.sys は AltConfigurationValue によって示される構成を指定することで別の選択構成要求を送信します。 代替の構成には、50 ミリアンペアが必要です。 またはより少ないとしないその他の問題が発生した、選択構成要求が正常に完了します。

### <a href="" id="compatibility-feature"></a> 互換性の機能

関数の複合デバイスでのクライアント ドライバーを複合デバイスの構成 を選択できない場合でもクライアント ドライバーがで、Usbccgp.sys に選択構成要求を送信できますも。 その要求を構築する方法については、次を参照してください。 [USB デバイスの構成の選択方法](how-to-select-a-configuration-for-a-usb-device.md)します。 Usbccgp.sys では、クライアント ドライバーから選択構成要求を受信した後、次のタスクを実行します。

1.  USB ポート ドライバーによって、選択構成要求の検証に使用する同じ条件を使用して、受信した要求を検証します。
2.  Usbccgp.sys が URB 型の URB を送信することによって選択インターフェイス要求を発行する場合は、要求では、現在の設定とは異なるインターフェイスまたはパイプの設定を指定します、\_関数\_選択\_インターフェイスを変更するには新しいインターフェイスとパイプの設定を既存の設定。
3.  キャッシュの内容をコピー、 [ **USBD\_インターフェイス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff539068)と[ **USBD\_パイプ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff539114) URB に構造体。
4.  URB を完了します。

## <a name="related-topics"></a>関連トピック
[USB デバイスの構成を選択する方法](how-to-select-a-configuration-for-a-usb-device.md)  
[USB デバイスの構成](configuring-usb-devices.md)  



