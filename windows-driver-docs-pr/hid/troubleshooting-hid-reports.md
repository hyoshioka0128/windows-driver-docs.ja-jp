---
title: HID レポートのトラブルシューティング
description: HID レポートのトラブルシューティング
ms.assetid: 8fbf641b-461b-44c2-9cc5-c1547abc75d6
keywords:
- HID レポート WDK、トラブルシューティング
- WDK HID、トラブルシューティングを報告します。
- レポートのトラブルシューティング WDK HID
- HID レポートが削除されました WDK
- エラー WDK HID レポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d433ee89e0a72f0f080cd40b340648de89271cec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841550"
---
# <a name="troubleshooting-hid-reports"></a>HID レポートのトラブルシューティング





ここでは、 [HID 使用法](hid-usages.md)を抽出または設定しようとしたときに、ユーザーモードアプリケーションとカーネルモードドライバーが発生する可能性がある、次のような最も一般的な問題について説明します。

[HID レポート ID エラー](#hid-report-id-errors)

[破棄された HID レポート](#dropped-hid-reports)

### <a href="" id="hid-report-id-errors"></a>HID レポート ID エラー

アプリケーションまたはドライバーが HID コレクションから HID レポートを受信する場合は、コレクションに含まれている任意のレポートを指定できます (コレクションは任意の順序でレポートを返すことができるため)。 **Hidp\_Get * * * Xxx*ルーチンでは、次の状態値が返されます。これは、レポート ID エラーを示しています。

<a href="" id="hidp-status-incompatible-report-id"></a>HIDP\_状態\_互換性のない\_レポート\_ID  
要求された使用量は、HID コレクションでサポートされているレポートに含まれていますが、アプリケーションまたはドライバーによって指定されたレポートには含まれていません。

<a href="" id="hidp-status-usage-not-found"></a>HIDP\_状態\_使用状況\_\_見つかりませんでした  
要求された使用状況は、最上位レベルのコレクションでサポートされているレポートに含まれていません。

たとえば、次の図は、2つのレポートを含む HID コレクションを示しています。

![2つのレポートを含む hid コレクションを示す図](images/reportid.png)

この例に基づいて、アプリケーションまたはドライバーがコレクションからレポートを受信し、 [**Hidp\_Getの値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevalue)を呼び出して "value X" の現在の値を抽出するとします。 レポート ID が7の場合、このルーチンは、HIDP\_STATUS\_互換性のない\_レポート\_ID を返します。これは、デバイスが値 X をサポートしているが、その値 X がレポートに存在しないことを示します。 一方、アプリケーションまたはドライバーが "値 Z" の値を要求した場合、このルーチンは、\_が見つから\_ないことを示す HIDP\_ステータス\_使用状況を返します。これは、値 Z がコレクションでサポートされているレポートに含まれていないことを示します。

アプリケーションまたはドライバーで **Hidp\_set * * * Xxx*ルーチンを使用してレポートの使用法を設定すると、ルーチンは同じ2つの状態の値を返すこともできます。 HIDP\_STATUS\_USAGE\_の意味は、\_見つかりませんでしたが、**hidp\_Get * * Xxx*ルーチンと同じです。 ただし、HIDP\_ステータス\_互換性のない\_レポート\_ID の意味は異なります。 この状態値は、レポートが以前にレポート ID で構成されており、呼び出し元によって指定された使用がそのレポート ID に属していないことを示します。 前の図を例として使用すると、アプリケーションまたはドライバーが[**Hidp\_SetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)を使用してゼロで初期化されたレポートで "ボタン 2" を設定した後、レポート ID が7のレポートが構成されます。 その後、アプリケーションまたはドライバーが[**hidp\_setの値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevalue)を使用して同じレポートで "値 X" を設定しようとすると、ルーチンは、hidp\_STATUS\_互換性のない\_レポート\_ID を返します。

**Hidp\_** <em>XXX</em>ルーチンが hidp\_STATUS\_互換性のない\_レポート\_ID を返す場合、呼び出し元は次のいずれかのアクションを実行する必要があります。

-   呼び出し元が使用法を設定している場合は、正しい長さの新しいレポートを割り当て、ゼロを初期化してから、ルーチンを再度呼び出します。 呼び出し元は、レポート内のすべての使用状況を正常に設定した後に、レポートをコレクションに送信できます。

-   呼び出し元が使用状況を抽出している場合は、コレクションから取得した別のレポートを使用してルーチンを呼び出す必要があります。

### <a href="" id="dropped-hid-reports"></a>破棄された HID レポート

Hid[クライアントドライバー](hid-client-drivers.md)が hid コレクションから入力レポートを取得すると、そのレポートは hid クラスドライバーによって保持されているリングバッファーに格納されます。 このメカニズムにより、アプリケーションまたはドライバーが必要な入力レポートを見逃す可能性が低くなります。

既定では、HID クラスドライバーは32レポートを保持する入力レポートのリングバッファーを保持します。 コレクションが HID クラスドライバーにデータを送信する速度が、ユーザーモードアプリケーションやカーネルモードドライバーよりも速くなると、バッファーオーバーフローによって入力レポートが失われます。 バッファーオーバーフローの可能性を減らすために、アプリケーションまたはドライバーは、バッファーのサイズ (レポートの数) を再構成できます。 ドライバーは、 [**ioctl\_GET\_num\_デバイス\_入力\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_get_num_device_input_buffers) buffer 要求を使用してバッファーのサイズを取得して変更します。また、 [**ioctl\_設定\_デバイス\_入力\_13_ BUFFERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_set_num_device_input_buffers)要求。 アプリケーションは、 [**hidd\_getnuminputbuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getnuminputbuffers)と[**Hidd\_setnuminputbuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setnuminputbuffers)を呼び出すことによって同じ操作を実行します。

 

 




