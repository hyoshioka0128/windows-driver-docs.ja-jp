---
title: 現在のファイル位置の使用
description: 現在のファイル位置の使用
ms.assetid: d342d973-8fff-4d00-a275-114012c17727
keywords:
- ファイルの WDK カーネル
- ファイル オブジェクトの WDK カーネル
- WDK のオブジェクトのファイル オブジェクト
- ファイル ハンドルの WDK カーネル
- ファイルの WDK カーネルへのハンドルします。
- 現在のファイル位置の WDK カーネル
- ファイル位置の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3ae511843de7f97aeb74653250b7b15b35128e8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358184"
---
# <a name="using-the-current-file-position"></a>現在のファイル位置の使用





を作成またはファイルを開くときに、ファイル ハンドルに関連付けられている現在のファイル位置のポインターを作成する I/O マネージャーが発生することができます。 これを完了したら、読み取るし、ファイルの現在の位置にデータを書き込むことができ、I/O マネージャーが読み取りまたは書き込みバイト数で位置を自動的に更新が。

既定では、I/O マネージャーは、現在のファイル位置のポインターを保持しません。 この既定値は、効率性を提供します。-すべての読み取りを同期し、ファイル オブジェクトに対する書き込み操作に I/O マネージャー、現在のファイルの位置を正しく維持する必要があるためです。

関連付けられている現在のファイル位置ポインターを同期を指定するハンドルでのアクセスを作成する、 *DesiredAccess*パラメーターを[ **ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)、[ **IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatefile)、または[ **ZwOpenFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntopenfile)、いずれかのファイルと\_同期\_IO\_アラートまたはファイル\_同期\_IO\_で警告を発行しません、 *CreateOptions*または*OpenOptions*パラメーター。 ファイルも指定していないことを確認する\_APPEND\_データにアクセス権。

[**ZwReadFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntreadfile)と[ **ZwWriteFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntwritefile)操作によって影響を受けるデータの次の位置を指すように、現在のファイル位置のポインターを自動的に更新します。 たとえば、バイトで始まる 20 のバイトを読み取る場合は、オフセット 101、 **ZwReadFile** 121 に現在の位置を更新します。

確認または呼び出すことで、現在のファイルの位置を変更することができます[ **ZwQueryInformationFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntqueryinformationfile)または[ **ZwSetInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntsetinformationfile)、それぞれします。 いずれの場合も、設定、 *FileInformationClass*パラメーターを**FilePositionInformation**します。

 

 




