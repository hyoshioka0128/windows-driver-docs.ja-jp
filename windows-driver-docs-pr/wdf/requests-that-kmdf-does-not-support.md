---
title: KMDF でサポートされていない要求
description: KMDF でサポートされていない要求
ms.assetid: 1C23BD32-FD55-4D35-B23D-0B320E3DEDF3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f1938f30ed97cd304ea076197ce9a6c81180a0d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376280"
---
# <a name="requests-that-kmdf-does-not-support"></a>KMDF でサポートされていない要求


\[KMDF にのみ適用されます。\]

カーネル モード ドライバー フレームワーク (KMDF) は、次の主要なコードの IRP の I/O 要求をサポートしていません。

-   IRP\_MJ\_作成\_"メール スロット"

-   IRP\_MJ\_作成\_名前付き\_パイプ

-   IRP\_MJ\_デバイス\_変更

-   [**IRP\_MJ\_ディレクトリ\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-directory-control)

-   [**IRP\_MJ\_ファイル\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-file-system-control)

-   [**IRP\_MJ\_フラッシュ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)

-   [**IRP\_MJ\_ロック\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-lock-control)

-   [**IRP\_MJ\_クエリ\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-ea)

-   [**IRP\_MJ\_クエリ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-query-information)

-   [**IRP\_MJ\_クエリ\_クォータ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-quota)

-   [**IRP\_MJ\_QUERY\_SECURITY**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-security)

-   [**IRP\_MJ\_クエリ\_ボリューム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-volume-information)

-   [**IRP\_MJ\_SET\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-ea)

-   [**IRP\_MJ\_SET\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-set-information)

-   [**IRP\_MJ\_SET\_QUOTA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-quota)

-   [**IRP\_MJ\_SET\_SECURITY**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-security)

-   [**IRP\_MJ\_設定\_ボリューム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-volume-information)

フレームワークは、このような要求を受信したときに、既定のアクションは、要求の対象となったデバイス オブジェクトに依存します。 FDO または PDO は、フレームワークの完了ステータスがステータスの IRP\_無効な\_デバイス\_を要求します。 フィルター操作の場合は、フレームワークは、[次へ] の下のドライバーに IRP を渡します。 フレームワークは、これらの要求の種類をサポートしていない、KMDF ドライバーでもに処理できます。 詳細については、次を参照してください。[処理フレームワークがサポートされていない IRP](handling-an-irp-that-the-framework-does-not-support.md)します。

 

 





