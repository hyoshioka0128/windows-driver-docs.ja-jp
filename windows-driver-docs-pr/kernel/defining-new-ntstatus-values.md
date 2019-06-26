---
title: 新しい NTSTATUS 値の定義
description: 新しい NTSTATUS 値の定義
ms.assetid: 44211ae4-6bfe-4931-b12c-e590c7aacd97
keywords:
- NTSTATUS 値 WDK カーネル
- カスタムの NTSTATUS 値 WDK カーネル
- IO_ERR_XXX 値
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a5ac52eed79aaa0dc3da86b68bbcc2aa776374d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377104"
---
# <a name="defining-new-ntstatus-values"></a>新しい NTSTATUS 値の定義





ドライバーは、カスタムの IO を定義できます\_ERR\_*XXX*として使用する定数**ErrorCode**エラーのログ記録の値します。 一緒に記述されているドライバーのペアは、カスタムの状態を定義できますも\_*XXX*値[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)要求。

次の図は、32 ビットの NTSTATUS 値のビット フィールドを示します。

![ntstatus 値のビット フィールドを示す図](images/16ntstat.png)

**重大度**上の図に示すようにフィールドを次のシステム定義の値のいずれかを指定する必要があります、重大度コードを示します。

<a href="" id="status-severity-success"></a>ステータス\_重大度\_成功  
状態など、成功した NTSTATUS 値を示します\_成功した場合、または値 IO\_ERR\_再試行\_パケットのエラー ログに成功しました。

<a href="" id="status-severity-informational"></a>ステータス\_重大度\_情報  
状態などの情報の NTSTATUS 値を示します\_シリアル\_詳細\_を書き込みます。

<a href="" id="status-severity-warning"></a>ステータス\_重大度\_警告  
警告の状態などの NTSTATUS 値を示します\_デバイス\_用紙\_空です。

<a href="" id="status-severity-error"></a>ステータス\_重大度\_エラー  
エラー状態などの NTSTATUS 値を示す\_不十分\_のリソースを**FinalStatus**値または IO\_ERR\_構成\_のエラー**ErrorCode**パケットのエラー ログ内の値。

ほとんどのパブリック IO\_ERR\_*XXX*ステータスに定数が属している\_重大度\_エラー カテゴリ。

**施設**コードがエラーを生成するための機能を指定します。 新しい IO の\_ERR\_*XXX*値、ドライバー、機能を指定する\_IO\_エラー\_のコード値**施設**します。 カスタム状態の\_*XXX*値は、さまざまな値の意味**施設**ドライバーで定義されます。

**C**ビットのかどうか、値は顧客によって定義された、または Microsoft 定義を指定します。 ビットは、顧客によって定義された値、および Microsoft 定義の値のチェック ボックスをオフに設定されています。

ドライバーは、新しい IO を定義できます\_ERR\_*XXX*システム イベント ログ内のカスタム エラー メッセージを識別する値。 NTSTATUS 値とそのユーザーを識別するエラー メッセージを定義する方法については、次を参照してください。[カスタム エラーの種類を定義する](defining-custom-error-types.md)します。

ドライバーのペアは、ドライバー固有の状態を定義できます\_*XXX*に関する情報を非公開で通信するために値が定義されている[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)ペアの以上のドライバーを下から要求します。

クラス ドライバーは、すべてのプライベート状態をマップする必要があります\_*XXX*値を既存のより高度なドライバーの場合、IRP を完了したときにシステム定義 NTSTATUS 値[ *IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)その IRP のルーチンを呼び出すことがあります。

ペアの表示とビデオのミニポート ドライバー、ビデオ ポート ドライバーにはパブリック状態の間のマッピング\_*XXX*値およびビデオのミニポート ドライバーによって返される Win32 定義されている定数。 詳細については、次を参照してください。 [Windows 2000 Display Driver Model でのビデオのミニポート ドライバー](https://docs.microsoft.com/windows-hardware/drivers/display/video-miniport-drivers-in-the-windows-2000-display-driver-model)します。

ドライバーは、システム定義の値のみを Win32 エラー コードに変換できるため、ユーザー モードで受信可能な Irp の NTSTATUS のカスタム値を使用できません。

 

 




