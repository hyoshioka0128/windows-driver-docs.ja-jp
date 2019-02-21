---
title: 現在の位置を使用します。
description: 現在の位置を使用します。
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
ms.openlocfilehash: 6d1fc467973915a96aa87b646c0784561f1423c2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529651"
---
# <a name="using-the-current-file-position"></a>現在の位置を使用します。





を作成またはファイルを開くときに、ファイル ハンドルに関連付けられている現在のファイル位置のポインターを作成する I/O マネージャーが発生することができます。 これを完了したら、読み取るし、ファイルの現在の位置にデータを書き込むことができ、I/O マネージャーが読み取りまたは書き込みバイト数で位置を自動的に更新が。

既定では、I/O マネージャーは、現在のファイル位置のポインターを保持しません。 この既定値は、効率性を提供します。-すべての読み取りを同期し、ファイル オブジェクトに対する書き込み操作に I/O マネージャー、現在のファイルの位置を正しく維持する必要があるためです。

関連付けられている現在のファイル位置ポインターを同期を指定するハンドルでのアクセスを作成する、 *DesiredAccess*パラメーターを[ **ZwCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff566424)、[ **IoCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff548418)、または[ **ZwOpenFile**](https://msdn.microsoft.com/library/windows/hardware/ff567011)、いずれかのファイルと\_同期\_IO\_アラートまたはファイル\_同期\_IO\_で警告を発行しません、 *CreateOptions*または*OpenOptions*パラメーター。 ファイルも指定していないことを確認する\_APPEND\_データにアクセス権。

[**ZwReadFile** ](https://msdn.microsoft.com/library/windows/hardware/ff567072)と[ **ZwWriteFile** ](https://msdn.microsoft.com/library/windows/hardware/ff567121)操作によって影響を受けるデータの次の位置を指すように、現在のファイル位置のポインターを自動的に更新します。 たとえば、バイトで始まる 20 のバイトを読み取る場合は、オフセット 101、 **ZwReadFile** 121 に現在の位置を更新します。

確認または呼び出すことで、現在のファイルの位置を変更することができます[ **ZwQueryInformationFile** ](https://msdn.microsoft.com/library/windows/hardware/ff567052)または[ **ZwSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567096)、それぞれします。 いずれの場合も、設定、 *FileInformationClass*パラメーターを**FilePositionInformation**します。

 

 




