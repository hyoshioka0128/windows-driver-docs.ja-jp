---
title: 事前解析データを取得する
description: 事前解析データを取得する
ms.assetid: 7a2bdbd1-a970-421f-bbaa-40fe589bb49a
keywords:
- コレクション WDK HID、preparsed data
- HID コレクション WDK, preparsed data
- preparsed data WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9eedd7df5eb1ecebcbe55a1b5959f7fd6395462a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841564"
---
# <a name="obtaining-preparsed-data"></a>事前解析データを取得する





このセクションでは、ユーザーモードアプリケーションとカーネルモードドライバーが HID コレクションの[preparsed データ](preparsed-data.md)を取得する方法について説明します。このデータは、コレクションの hid レポートを記述する不透明な構造です。

### <a name="user-mode-application"></a>ユーザーモードアプリケーション

ユーザーモードアプリケーションは、preparsed データを必要とする[HIDClass サポートルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を呼び出す前に、コレクションの preparsed データを取得する必要があります。 アプリケーションは、デバイス上に開いているファイルがある限り、コレクションの preparsed データへのアクセスを保持する必要があります。

HID コレクションでファイルを開いた後、アプリケーションは、 [**Hidd\_GetPreparsedData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getpreparseddata)を呼び出して、定期的に割り当てられたバッファーにコレクションの preparsed データを返します。

アプリケーションがコレクションへのアクセスを必要としなくなったときに、アプリケーションは、 [**Hidd\_FreePreparsedData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_freepreparseddata)を呼び出す必要があります。

### <a name="kernel-mode-driver"></a>カーネルモードドライバー

カーネルモードドライバーが HID コレクションを開くと、ドライバーは次の方法でコレクションの[preparsed データ](preparsed-data.md)を取得します。

-   コレクションの preparsed データの長さを取得します。

-   コレクションの preparsed データを取得します。

Preparsed データの長さを確認するために、ドライバーは[ **\_コレクション\_情報要求\_IOCTL\_HID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_get_collection_information)を使用します。 この要求は、 [**HID\_COLLECTION\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ns-hidclass-_hid_collection_information)構造体を返します。 この構造体の**記述子サイズ**のメンバーは、コレクションの preparsed データのサイズをバイト単位で指定します。 ドライバーは、preparsed データを保持するために、少なくともこのサイズの非ページプールからバッファーを割り当てる必要があります。

Preparsed データのバッファーを割り当てた後、ドライバーは、preparsed データを取得するために\_コレクション\_記述子要求を使用して、 [**IOCTL\_HID\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_get_collection_descriptor)を使用します。

Preparsed データを取得した後、ドライバーはこのデータを**Hidp\_** <em>Xxx</em> HID サポートルーチンと共に使用して、hid コレクションの機能に関する情報を取得したり、hid レポートからコントロールデータを抽出したりできます。

 

 




