---
title: RunAs
description: RunAs
ms.assetid: 47183A50-513C-4bc5-8DC4-33065323F584
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52a8be4e9412f4c06df88ed2133d9425fed43f56
ms.sourcegitcommit: f63852446e614c985a65f599cdfe788bdb0c6089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2020
ms.locfileid: "87425732"
---
# <a name="runas"></a>RunAs

TAEF は、ローカルシステムとして、または低整合性プロセス内で、昇格、制限、テストを実行するためのメカニズムを提供します。

## <a name="prerequisites"></a>前提条件

- 管理者特権のないプロセスから管理者特権でのテストを実行したり、昇格されたプロセスから管理者以外のテストを実行したり、テストをローカルシステムとして実行したりするには、コンピューターにサービスをインストールして実行する必要があり[ます。](te-service.md)

## <a name="runas-types"></a>RunAs の種類

TAEF では、テストメタデータまたはコマンドプロンプトを使用して指定される次の種類の RunAs がサポートされています。

- [RunAs Elevated](runas-elevated.md)
- [RunAs LowIL](runas-lowil.md)
- [RunAs Restricted](runas-restricted.md)
- [RunAs System](runas-system.md)
