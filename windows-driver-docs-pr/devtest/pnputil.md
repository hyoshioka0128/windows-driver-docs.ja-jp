---
title: PnPUtil
description: PnPUtil
ms.assetid: 3678fd41-c3ee-4538-b783-6f099ac104a6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9556127d2cc0be3ba5188dcdfdf7ed8655f53d9
ms.sourcegitcommit: 34a06eda78c8d935f3900b86fa0f620027bc6577
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83778346"
---
# <a name="pnputil"></a>PnPUtil

PnPUtil (PnPUtil) は、管理者が[ドライバーパッケージ](../install/driver-packages.md)に対してアクションを実行できるようにするコマンドラインツールです。  次に例をいくつか示します。

- ドライバーパッケージを[ドライバーストア](../install/driver-store.md)に追加します。

- コンピューターにドライバーパッケージをインストールします。

- ドライバーストアからドライバーパッケージを削除します。

- 現在ドライバーストアにあるドライバーパッケージを列挙します。 インボックスパッケージ以外のドライバーパッケージのみが一覧表示されます。 *インボックス*ドライバーパッケージは、Windows またはそのサービスパックの既定のインストールに含まれています。

## <a name="where-can-i-download-pnputil"></a>PnPUtil はどこでダウンロードできますか。

PnPUtil は、windows Vista (ディレクトリ内) 以降のすべてのバージョンの Windows に含まれてい `%windir%\system32` ます。 個別の PnPUtil ダウンロードパッケージがありません。

- **コマンドプロンプト**ウィンドウを開きます ([**管理者として実行**])。
- `pnputil /?`コマンドオプションを表示するには、「」と入力します。 詳細については、「 [**PnPUtil コマンドの構文**](pnputil-command-syntax.md)」を参照してください。

> [!NOTE]
> PnPUtil は、Windows Vista 以降のバージョンの Windows でサポートされています。 Windows XP では、PnPUtil は使用できませんが、[ドライバーインストールフレームワーク (DIFx)](../install/difx-guidelines.md)ツールを使用して、ドライバーパッケージのインストールを作成およびカスタマイズすることができます。
