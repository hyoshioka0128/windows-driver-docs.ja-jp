---
title: KMDF でサポートされていない要求
description: KMDF でサポートされていない要求
ms.assetid: 1C23BD32-FD55-4D35-B23D-0B320E3DEDF3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbae806198afcbe8fad8f43c2367ff86411daf73
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582523"
---
# <a name="requests-that-kmdf-does-not-support"></a>KMDF でサポートされていない要求


\[KMDF にのみ適用されます。\]

カーネル モード ドライバー フレームワーク (KMDF) は、次の主要なコードの IRP の I/O 要求をサポートしていません。

-   IRP\_MJ\_作成\_"メール スロット"

-   IRP\_MJ\_作成\_名前付き\_パイプ

-   IRP\_MJ\_デバイス\_変更

-   [**IRP\_MJ\_ディレクトリ\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff548658)

-   [**IRP\_MJ\_ファイル\_システム\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550751)

-   [**IRP\_MJ\_フラッシュ\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/ff550760)

-   [**IRP\_MJ\_ロック\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff549251)

-   [**IRP\_MJ\_クエリ\_EA**](https://msdn.microsoft.com/library/windows/hardware/ff549279)

-   [**IRP\_MJ\_クエリ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff550788)

-   [**IRP\_MJ\_クエリ\_クォータ**](https://msdn.microsoft.com/library/windows/hardware/ff549293)

-   [**IRP\_MJ\_QUERY\_SECURITY**](https://msdn.microsoft.com/library/windows/hardware/ff549298)

-   [**IRP\_MJ\_クエリ\_ボリューム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff549318)

-   [**IRP\_MJ\_SET\_EA**](https://msdn.microsoft.com/library/windows/hardware/ff549346)

-   [**IRP\_MJ\_SET\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff550799)

-   [**IRP\_MJ\_SET\_QUOTA**](https://msdn.microsoft.com/library/windows/hardware/ff549401)

-   [**IRP\_MJ\_SET\_SECURITY**](https://msdn.microsoft.com/library/windows/hardware/ff549407)

-   [**IRP\_MJ\_設定\_ボリューム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff549415)

フレームワークは、このような要求を受信したときに、既定のアクションは、要求の対象となったデバイス オブジェクトに依存します。 FDO または PDO は、フレームワークの完了ステータスがステータスの IRP\_無効な\_デバイス\_を要求します。 フィルター操作の場合は、フレームワークは、[次へ] の下のドライバーに IRP を渡します。 フレームワークは、これらの要求の種類をサポートしていない、KMDF ドライバーでもに処理できます。 詳細については、[処理フレームワークがサポートされていない IRP](handling-an-irp-that-the-framework-does-not-support.md)を参照してください。

 

 





