---
title: 新しい NTSTATUS 値の定義
description: 新しい NTSTATUS 値の定義
ms.assetid: 44211ae4-6bfe-4931-b12c-e590c7aacd97
keywords:
- NTSTATUS 値 WDK カーネル
- カスタム NTSTATUS 値 WDK カーネル
- IO_ERR_XXX の値
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 700726415ca037a4791361bb3bc19db720a61aa8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836967"
---
# <a name="defining-new-ntstatus-values"></a>新しい NTSTATUS 値の定義





ドライバーでは、エラーをログに記録するときに**ErrorCode**値として使用するカスタム IO\_ERR\_*XXX*定数を定義できます。 同時に記述されたドライバーのペアでは、 [**IRP\_MJ\_内部\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)要求のカスタムステータス\_*XXX*値を定義することもできます。

次の図は、32ビットの NTSTATUS 値のビットフィールドを示しています。

![ntstatus 値のビットフィールドを示す図](images/16ntstat.png)

上の図に示されている**重大度**フィールドは、次のシステム定義の値のいずれかである必要がある重大度コードを示しています。

<a href="" id="status-severity-success"></a>状態\_重要度\_成功  
正常な NTSTATUS 値 (STATUS\_SUCCESS など) を示します。または、エラーログパケットの ERR\_再試行\_成功した場合は、値 IO\_失敗します。

<a href="" id="status-severity-informational"></a>ステータス\_重要度\_情報  
ステータス\_シリアル\_その他の\_書き込みなど、情報ポートの値を示します。

<a href="" id="status-severity-warning"></a>ステータス\_重要度\_警告  
ステータス\_デバイス\_用紙\_空など、NTSTATUS 値の警告を示します。

<a href="" id="status-severity-error"></a>状態\_重要度\_エラー  
エラーログパケットの**ErrorCode**値について、 **finalstatus**値または IO\_ERR\_構成\_エラーの状態\_\_不足などのエラーの NTSTATUS 値を示します。

ほとんどのパブリック IO\_ERR\_*XXX*定数は、STATUS\_SEVERITY\_ERROR カテゴリに属しています。

**ファシリティ**コードは、エラーを生成したファシリティを指定します。 新しい IO\_ERR\_*XXX*の値については **、ファシリティ\_** のファシリティ\_エラーの\_コード値をドライバーが指定します。 カスタムステータス\_*XXX*値の場合、**ファシリティ**の異なる値の意味はドライバーで定義されています。

**C**ビットは、値が顧客定義または Microsoft 定義かどうかを指定します。 ビットは、ユーザー定義の値に対して設定され、Microsoft 定義の値に対してはクリアされます。

ドライバーは、システムイベントログでカスタムエラーメッセージを識別するために、新しい IO\_ERR\_*XXX*値を定義できます。 NTSTATUS 値およびそれらが識別するエラーメッセージを定義する方法の詳細については、「[カスタムエラーの種類の定義](defining-custom-error-types.md)」を参照してください。

ドライバーのペアは、ドライバー固有の状態\_*XXX*の値を定義して、プライベートに定義された[**IRP\_MJ\_内部\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)に関する情報を伝達し、下位のドライバーから上位のドライバーへの要求を制御することができます。ペアの。

クラスドライバーは、既存の上位レベルのドライバーの[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンがその irp に対して呼び出される可能性がある場合に、irp を完了するときに、プライベートステータス\_*XXX*値をシステム定義の NTSTATUS 値にマップする必要があります。

ビデオポートドライバーは、ペアリングされたディスプレイとビデオミニポートドライバーについて、パブリックステータス\_*XXX*値と、ビデオミニポートドライバーによって返される Win32 定義定数との間のマッピングを行います。 詳細については、「 [Windows 2000 Display Driver Model のビデオミニポートドライバー](https://docs.microsoft.com/windows-hardware/drivers/display/video-miniport-drivers-in-the-windows-2000-display-driver-model)」を参照してください。

ドライバーは、システム定義の値のみを Win32 エラーコードに変換できるため、ユーザーモードで受信できる Irp に対してカスタムの NTSTATUS 値を使用することはできません。

 

 




