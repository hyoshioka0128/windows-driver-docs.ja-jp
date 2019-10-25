---
title: 現在のファイル位置の使用
description: 現在のファイル位置の使用
ms.assetid: d342d973-8fff-4d00-a275-114012c17727
keywords:
- ファイル WDK カーネル
- ファイルオブジェクト WDK カーネル
- オブジェクト WDK ファイルオブジェクト
- ファイルが WDK カーネルを処理する
- WDK カーネルファイルへのハンドル
- 現在のファイルの位置 (WDK カーネル)
- ファイル位置 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b08b7ac9bc1bdc6d0fcf0aad254dd8b0017eac1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835866"
---
# <a name="using-the-current-file-position"></a>現在のファイル位置の使用





ファイルを作成または開くときに、ファイルハンドルに関連付けられている現在のファイル位置ポインターを i/o マネージャーで作成することができます。 この操作を完了すると、現在のファイルの位置に対するデータの読み取りと書き込みができるようになります。また、i/o マネージャーによって、読み取りまたは書き込みが行われたバイト数によって位置が自動的に更新されます。

既定では、i/o マネージャーは、現在のファイル位置ポインターを保持しません。 現在のファイルの位置を正しく維持するには、ファイルオブジェクトのすべての読み取り操作と書き込み操作を同期するために i/o マネージャーが必要となるため、この既定値は効率が向上します。

現在のファイル位置ポインターが関連付けられているハンドルを作成するには、 *DesiredAccess*パラメーターで、 [**zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)、 [**Iocreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)、または[**ZWCREATEFILE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntopenfile)に対するアクセスの同期権限を指定し、いずれかのファイル\_同期\_IO\_アラートまたはファイル\_*createoptions*パラメーターまたは*openoptions*パラメーターには、同期\_io\_非アラートがあります。 また、\_データアクセス権を追加\_ファイルを指定しないようにしてください。

[**Zwreadfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)と[**zwreadfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntwritefile)は、現在のファイルの位置ポインターを自動的に更新して、操作の影響を受けるデータだけを指し示すようにします。 たとえば、バイトオフセット101から始まる20バイトを読み取ると、 **Zwreadfile**は現在のファイルの位置を121に更新します。

[**Zwqueryinformationfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)または[**zwqueryinformationfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)を呼び出して、現在のファイルの位置を確認または変更できます。 どちらの場合も、 *Fileinformationclass*パラメーターを**fileinformationclass**に設定します。

 

 




