---
title: NT デバイス名
description: NT デバイス名
ms.assetid: dfcc7338-7c4d-4b4c-9a13-c76bfe82f5a9
keywords:
- NT デバイス名 WDK カーネル
- デバイスオブジェクト WDK カーネル、
- 名前付きデバイスオブジェクト WDK カーネル
- デバイス名 WDK カーネル
- 非 WDM ドライバーデバイス名 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fec5a5e0c1ba1c7ba440ad956b7f8d4deec8c281
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838542"
---
# <a name="nt-device-names"></a>NT デバイス名





名前付きデバイスオブジェクトには **\\device\\** <em>DeviceName</em>という形式の名前が付けられます。 これは、デバイスオブジェクトの*NT デバイス名*と呼ばれます。

### <a name="device-names-for-wdm-drivers"></a>WDM ドライバーのデバイス名

WDM ドライバーは、デバイスオブジェクトに直接名前を指定しません。 代わりに、デバイス名がドライバー間で競合しないようにするための一貫した名前付けスキームがシステムによって設定されます。 WDM ドライバーの命名規則は次のとおりです。

-   デバイスの PDO にはという名前が付けられます。 バスドライバーは、列挙するデバイスに対して PDOs という名前の要求を要求します。 バスドライバーは、デバイスオブジェクトを作成するときにデバイス\_名前のデバイスの特性\_自動生成\_ファイルを指定します。 詳細については、「[デバイスの特性の指定](specifying-device-characteristics.md)」を参照してください。 その後、システムによってデバイス名が自動的に生成されます。

-   FDOs とフィルター DOs の名前が指定されていません。 関数ドライバーとフィルタードライバーは、デバイスオブジェクトを作成するときに名前を要求しません。

名前付きデバイスオブジェクトに対するすべての i/o 要求は、そのデバイスオブジェクトのスタックの最上位のオブジェクトに自動的に移動します。 したがって、名前を付ける必要があるのは PDO だけです。 ユーザーモードのアプリケーションは、WDM デバイスオブジェクトを名前で参照しません。代わりに、アプリケーションはデバイス*インターフェイス*を介してデバイスオブジェクトにアクセスします。 詳細については、「[デバイスインターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)」を参照してください。

ドライバーライターは、デバイススタック内の複数のオブジェクトに名前を指定することはできません。 オペレーティングシステムは、指定されたオブジェクトに基づいてセキュリティ設定を確認します。 2つの異なるオブジェクトの名前が付けられ、セキュリティ記述子が異なる場合、弱いセキュリティ記述子を持つオブジェクトに送信される i/o 要求は、より強力なセキュリティ記述子を持つデバイスオブジェクトに接続できます。

### <a name="device-names-for-non-wdm-drivers"></a>WDM 以外のドライバーのデバイス名

非 WDM ドライバーは、任意の名前付きデバイスオブジェクトの名前を明示的に指定する必要があります。 ドライバーは、i/o 要求を受信するために、 **\\デバイス**オブジェクトディレクトリに少なくとも1つの名前付きデバイスオブジェクトを作成する必要があります。 デバイスオブジェクトを作成するときに、ドライバーはデバイス[**名を**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure) *DeviceName*パラメーターとして指定します。

 

 




