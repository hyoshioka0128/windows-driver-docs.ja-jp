---
title: HID レポートのトラブルシューティング
description: HID レポートのトラブルシューティング
ms.assetid: 8fbf641b-461b-44c2-9cc5-c1547abc75d6
keywords:
- HID WDK、レポートのトラブルシューティング
- WDK を非表示にレポートのトラブルシューティング
- WDK の HID レポートのトラブルシューティング
- 削除された HID レポート WDK
- WDK の HID レポートのエラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a668f4a72cf44ca47e9c454178da2e4bf8d797a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531114"
---
# <a name="troubleshooting-hid-reports"></a>HID レポートのトラブルシューティング





このセクションには、ユーザー モード アプリケーションとカーネル モード ドライバーを抽出または設定しようとしていますときに発生可能性がある次の最も一般的な問題がについて説明します[HID の使用](hid-usages.md):。

[HID レポート ID エラー](#hid-report-id-errors)

[HID レポートの削除](#dropped-hid-reports)

### <a href="" id="hid-report-id-errors"></a> HID レポート ID エラー

アプリケーションまたはドライバー HID レポート HID コレクションから受け取ると、(このコレクションは、任意の順序でレポートを返すことができます) ため、コレクションに含まれるすべてのレポートがあります。 **HidP\_取得 * * * Xxx*ルーチンは次の状態の値は、レポート ID のエラーを示すを返します。

<a href="" id="hidp-status-incompatible-report-id"></a>HIDP\_状態\_互換性のない\_レポート\_ID  
要求の使用法とは、HID コレクションでサポートされているレポートが、アプリケーションまたはドライバーが指定されているレポートではなくです。

<a href="" id="hidp-status-usage-not-found"></a>HIDP\_状態\_使用状況\_いない\_が見つかりました  
要求の使用法は、最上位のコレクションでサポートされているすべてのレポートではありません。

たとえば、2 つのレポートを含む HID コレクションは次の図のようにします。

![2 つのレポートを含む hid のコレクションを示す図](images/reportid.png)

この例に基づいて、アプリケーションを想定していますか、ドライバー、および呼び出しのコレクションからレポートを受信する[ **HidP\_GetUsageValue** ](https://msdn.microsoft.com/library/windows/hardware/ff539748) 「値 X」の現在の値を抽出するには レポートの ID が 7 の場合は、返されます HIDP\_状態\_互換性のない\_レポート\_ID で、デバイスが値の X をサポートしていますが、値 X がレポートに存在しないことを示します。 その一方で、アプリケーションまたはドライバーは、"値 Z"の値を要求している場合、ルーチンを返します HIDP\_状態\_使用状況\_いない\_値 Z がでサポートされているすべてのレポートでないことを示すが見つかりました、コレクションです。

アプリケーションまたはドライバーが使用している場合 **HidP\_設定 * * * Xxx*ルーチンも、ルーチンは、レポートの使用法を設定するには、同じ 2 つの状態値が返されます。 HIDP の意味\_状態\_使用状況\_いない\_が見つかりましたと同じ、**HidP\_取得 * * * Xxx*ルーチン。 ただし、HIDP の意味\_状態\_互換性のない\_レポート\_ID が異なります。 この状態値は、レポートは、レポートの id では、以前に構成された、呼び出し元によって指定された使用状況がレポート ID に属していないことを示します。 使用例として、前の図を使用して、アプリケーションやドライバーの後[ **HidP\_SetUsages** ](https://msdn.microsoft.com/library/windows/hardware/ff539792)をゼロで初期化されたレポート内の「ボタン 2」を設定する、レポートのレポート id の構成7 つです。 場合は、アプリケーションまたはドライバーが、その後使用を試みます[ **HidP\_SetUsageValue** ](https://msdn.microsoft.com/library/windows/hardware/ff539797)を同じレポート内の"値 X"を設定するルーチンが HIDP を返す\_状態\_互換性のない\_レポート\_id。

場合、 **HidP\_**<em>Xxx</em>ルーチン返します HIDP\_状態\_互換性のない\_レポート\_ID、呼び出し元は、のいずれか、次の操作:

-   場合は、呼び出し元は、使用法を設定する必要があります、正しい長さの新しいレポートを割り当てる、ゼロ初期化およびルーチンを再度呼び出します。 呼び出し元は、レポートですべての使用状況を正常に設定した後、コレクションにレポートを送信できます。

-   場合は、呼び出し元は、使用法を抽出は、コレクションから取得した別のレポートに、ルーチンを呼び出すことが必要があります。

### <a href="" id="dropped-hid-reports"></a> HID レポートの削除

ときに、[クライアント ドライバーを非表示に](hid-client-drivers.md)入力を取得、HID コレクションからレポートをレポートは、HID クラス ドライバーによって管理されるリング バッファーに格納されます。 このメカニズムは、アプリケーション、ドライバーが必要な入力のレポートを見逃すこと可能性を低減します。

既定では、HID クラス ドライバーは、32 のレポートを保持する入力レポート リング バッファーを保持します。 コレクションがユーザー モード アプリケーションよりも高速 HID クラス ドライバーにデータを転送またはカーネル モード ドライバーは、バッファーから取得、レポートの入力は失われますバッファーがオーバーフローしたため。 バッファーの可能性を低減するには、オーバーフロー、アプリケーション、ドライバーは、サイズ、バッファーのレポートの数を再構成できます。 ドライバーを取得しを使用して、バッファーのサイズを変更、 [ **IOCTL\_取得\_NUM\_デバイス\_入力\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff541058)要求および[ **IOCTL\_設定\_NUM\_デバイス\_入力\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff542087)要求。 アプリケーションが呼び出すことによって、同じ操作を行います[ **HidD\_GetNumInputBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff539675)と[ **HidD\_SetNumInputBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff539686).

 

 




