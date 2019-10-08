---
title: システムによって提供されるデバイスのインストールコンポーネント
description: システムによって提供されるデバイスのインストールコンポーネント
ms.assetid: faf586b9-ab99-4fee-a0d1-923000000189
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: a736de631067e947e9c47ef6cf9b3400a2a125c8
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007595"
---
# <a name="system-provided-device-installation-components"></a>システムによって提供されるデバイスのインストールコンポーネント


次の一覧では、Windows オペレーティングシステムによって提供されるデバイスインストールコンポーネントについて説明します。

<a href="" id="plug-and-play--pnp--manager"></a>プラグアンドプレイ (PnP) マネージャー  
プラグアンドプレイ (PnP) マネージャーは、Windows 内の PnP 機能に対して次のサポートを提供します。

-   システムの起動中のデバイスの検出と列挙
-   システムの実行中にデバイスを追加または削除する

詳細については、「 [PnP マネージャー](pnp-manager.md)」を参照してください。

<a href="" id="setupapi"></a>Setupapi.log  
セットアップアプリケーションプログラミングインターフェイス (*setupapi.log*) には、一般的なセットアップ機能 (**セットアップ * **xxx*) とデバイスインストール機能 (** Setupdi * **Xxx*および **Di * * * xxx*) が含まれています。 これらの関数は、INF ファイルの検索、デバイスのドライバーの候補リストの作成、ドライバーファイルのコピー、レジストリへの情報の書き込み、デバイスの共同インストーラーの登録など、多くのデバイスインストールタスクを実行します。 その他のデバイスインストールコンポーネントの多くは、これらの機能を呼び出します。

詳細については、「 [setupapi.log](setupapi.md)」を参照してください。

<a href="" id="configuration-manager-api"></a>Configuration Manager API  
PnP 構成マネージャー API は、Setupapi.log によって提供されない基本的なインストールと構成の操作を提供します。 PnP 構成マネージャーの関数は、デバイスノードの状態 (*devnode*) の取得やリソース記述子の管理などの低レベルのタスクを実行します。 これらの関数は、主に Setupapi.log によって呼び出されますが、他のデバイスインストールコンポーネントから呼び出すこともできます。

<a href="" id="driver-store"></a>ドライバーストア  
Windows Vista 以降では、ドライバーストアは、インボックスおよびサードパーティの[ドライバーパッケージ](driver-packages.md)の信頼されたコレクションです。 オペレーティングシステムは、このコレクションをローカルハードディスク上の安全な場所に保持します。 デバイスにインストールできるのは、ドライバーストア内のドライバーパッケージだけです。

詳細については、「[ドライバーストア](driver-store.md)」を参照してください。

<a href="" id="device-manager"></a>デバイス マネージャー  
デバイスマネージャーを使用すると、システム上のデバイスを表示および管理できます。 たとえば、デバイスの状態を表示したり、デバイスのプロパティを設定したりできます。

詳細については、「 [Using デバイスマネージャー](using-device-manager.md)」を参照してください。 また、デバイスマネージャーのヘルプドキュメントを参照してください。

 

 





