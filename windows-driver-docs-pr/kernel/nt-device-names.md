---
title: NT デバイス名
description: NT デバイス名
ms.assetid: dfcc7338-7c4d-4b4c-9a13-c76bfe82f5a9
keywords:
- NT のデバイス名の WDK カーネル
- という名前のデバイス オブジェクトの WDK カーネル
- 名前付きのデバイス オブジェクトの WDK カーネル
- デバイス名の WDK カーネル
- 非 WDM ドライバー デバイス名の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 876d89e35d1a7ab26a7aad7685574fb399e76e52
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365451"
---
# <a name="nt-device-names"></a>NT デバイス名





名前付きのデバイス オブジェクトが、フォームの名前を持つ **\\デバイス\\** <em>DeviceName</em>します。 これと呼ばれますが、 *NT デバイス名*デバイス オブジェクトの。

### <a name="device-names-for-wdm-drivers"></a>WDM ドライバーのデバイス名

WDM ドライバーは、デバイス オブジェクトを直接指定していません。 代わりに、システムが提供する名前付けスキームが確実にそのデバイス ドライバーの間に名前が競合しない一貫しました。 WDM ドライバーの名前付けスキームは次のとおりです。

-   デバイスの PDO をという名前です。 バス ドライバーでは、デバイスが列挙の名前付きの Pdo を要求します。 バス ドライバー ファイルを指定する\_自動生成された\_デバイス\_デバイス オブジェクトを作成するときにデバイスの特性を名します。 詳細については、次を参照してください。[デバイスの特性を指定する](specifying-device-characteristics.md)します。 自動的に生成されます、デバイス名。

-   Fdo とフィルター、DOs の名前はありません。 関数とフィルター ドライバーは、デバイス オブジェクトを作成するときに名前を要求しません。

名前付きのデバイス オブジェクトへの I/O 要求は、そのデバイス オブジェクトのスタックの一番上のオブジェクトに自動的に移動します。 したがって、PDO だけでは、名前を指定する必要があります。 ユーザー モード アプリケーションは名前で WDM デバイス オブジェクトを参照しません。アプリケーションが使用して、デバイス オブジェクトにアクセスする代わりに、その*デバイス インターフェイス*します。 詳細については、次を参照してください。[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)します。

ドライバー作成者には、デバイス スタックの 1 つ以上のオブジェクトは名前する必要があります。 オペレーティング システムは、名前付きのオブジェクトに基づくセキュリティ設定を確認します。 2 つの異なるオブジェクトを指定し、別のセキュリティ記述子は場合より強度の低いセキュリティ記述子を使用してオブジェクトに送信される I/O 要求より強力なセキュリティ記述子を持つデバイス オブジェクトにアクセスできます。

### <a name="device-names-for-non-wdm-drivers"></a>非 WDM ドライバー用のデバイス名

非 WDM ドライバーでは、すべてのデバイスの名前付きオブジェクトの名前を明示的に指定する必要があります。 ドライバーで少なくとも 1 つの名前付きのデバイス オブジェクトを作成する必要があります、 **\\デバイス**I/O 要求を受信するオブジェクトのディレクトリ。 ドライバーとデバイスの名前を指定します、 *DeviceName*パラメーターを[ **IoCreateDeviceSecure** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)デバイス オブジェクトを作成するときにします。

 

 




