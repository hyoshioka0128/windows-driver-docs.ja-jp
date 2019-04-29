---
title: ストレージ ドライバーのシステム ヘッダー ファイル
description: ストレージ ドライバーのシステム ヘッダー ファイル
ms.assetid: 2ee83fa4-41df-403e-86b8-b269f5dfbfed
keywords:
- ストレージ ドライバー WDK、システム ヘッダー ファイル
- ヘッダー ファイルの WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 780d4af5f6f9135cfce23cfde3fcde1e4b91b765
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390213"
---
# <a name="system-header-files-for-storage-drivers"></a>ストレージ ドライバーのシステム ヘッダー ファイル


## <span id="ddk_system_header_files_for_storage_drivers_kg"></span><span id="DDK_SYSTEM_HEADER_FILES_FOR_STORAGE_DRIVERS_KG"></span>


システムが指定したストレージ ドライバーは、ヘッダー ファイルをインクルード*scsi.h*SCSI 準拠のほとんどのドライバーでその他の構造が使用される、Cdb の SCSI 準拠の定義が含まれます。 このヘッダー ファイルが含まれる*srb.h*次の下位の記憶域クラスおよびフィルター ドライバーにシステムが指定したポート ドライバーによって提供されるインターフェイスを定義します。

NT ベースのオペレーティング システムのすべてのプラットフォームと x86 専用の Microsoft Windows システムの両方を実行する設計することができます、オペレーティング システムに依存しない SCSI ミニポート ドライバーがシステム提供のヘッダー ファイルをインクルード*miniport.h*と*scsi.h*、含む*srb.h*します。

テープ miniclass ドライバーが含まれる*minitape.h*します。

メディア チェンジャー miniclass ドライバーが含まれる*mcd.h*します。

クラスとフィルター ドライバーのベンダーから提供されたサンプル ファイルを組み込むことも*classpnp.h*と*classpnp.c*します。 これらのファイルは一連の定義**クラス**Xxx ルーチンをクラスおよびフィルター ドライバーの設計を簡略化します。 ただし、 *classpnp.h*と*classpnp.c*のみのサンプルは、任意のバージョンの Windows オペレーティング システムでサポートされていません。 に慎重に運用環境のドライバーでは、これらのファイルを使用するいくつかの構造とルーチン宣言の*classpnp.h*現在はないか、ドライバーで実行する Windows のバージョンと互換性がない可能性があります。

 

 




