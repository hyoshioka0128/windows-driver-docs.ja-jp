---
title: オブジェクト ディレクトリ
description: オブジェクト ディレクトリ
ms.assetid: b0e0d077-6736-4a54-b1eb-a30962442942
keywords:
- オブジェクトディレクトリ WDK カーネル
- 名前付きオブジェクト WDK カーネル
- ディレクトリ WDK オブジェクト
- 最上位レベルのオブジェクトディレクトリ WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc6247d159e47de931911ae75ae5cce0540d2269
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827769"
---
# <a name="object-directories"></a>オブジェクト ディレクトリ





*オブジェクトディレクトリ*は、他の名前付きオブジェクトを格納するためだけに使用される名前付きオブジェクトです。 たとえば、 **\\デバイス**オブジェクトディレクトリには、ドライバーによって作成された名前付きデバイスオブジェクトが格納されます。

オブジェクトディレクトリとファイルシステムディレクトリを混同しないようにしてください。 オブジェクトディレクトリは、オブジェクトマネージャー内にのみ存在し、ディスク上のディレクトリには対応していません。 (実際にはファイルシステムディレクトリは、ファイルオブジェクトとして表されます)。

次に示すのは、ドライバーが作成または使用する可能性のあるオブジェクトが含まれている最上位レベルのオブジェクトディレクトリの一覧です。

-   **\\コールバック**

    システムは、このディレクトリに標準コールバックオブジェクトを作成します。 詳細については、「[システム定義のコールバックオブジェクトの使用](using-a-system-defined-callback-object.md)」を参照してください。

-   **\\デバイス**

    ドライバーは、このディレクトリに名前付きデバイスオブジェクトを作成します。 詳細については、「[名前付きデバイスオブジェクト](named-device-objects.md)」を参照してください。

-   **\\KernelObjects**

    システムによって、このディレクトリに標準イベントオブジェクトが作成されます。 詳細については、「[標準イベントオブジェクト](standard-event-objects.md)」を参照してください。

-   **\\DosDevices**

    このディレクトリには、デバイスの MS-DOS デバイス名が、対応するデバイスオブジェクトへのシンボリックリンクとして格納されます。 詳細については、「 [MS-DOS デバイス名](ms-dos-device-names.md)」を参照してください。

システムは、他の最上位レベルのディレクトリを作成しますが、システムで使用するために予約されています。

ドライバーは、 [**Zwcreatedirectoryobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatedirectoryobject)ルーチンを呼び出すことによって、新しいオブジェクトディレクトリを作成できます。

 

 




