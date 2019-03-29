---
title: 廃止された関数のマクロ定義
description: 廃止された関数のマクロ定義
ms.assetid: 3d69b089-4875-4860-b5eb-3b5edcf3fc89
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c08e5bec3f1460f48c08e00065062e8fe4f043d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581737"
---
# <a name="macro-definitions-for-obsolete-functions"></a>廃止された関数のマクロ定義


## <span id="ddk_macro_definitions_for_obsolete_functions_ks"></span><span id="DDK_MACRO_DEFINITIONS_FOR_OBSOLETE_FUNCTIONS_KS"></span>


ヘッダー ファイルの portcls.h は、従来のドライバーのコードをコンパイルするソース ファイルの編集に必要とせずにいくつかを支援するマクロを定義します。 これらのマクロは、PortCls とカーネル モード ドライバーの機能が新しい PortCls への呼び出しとカーネル モード ドライバーの機能を廃止された呼び出しを簡単に置き換えます。 廃止された関数への参照を含む古いソース コードがあれば、新しい関数を呼び出す実行可能コードを作成するためのソース ファイルを再コンパイルするのに portcls.h でマクロを使用することができます。

次のトピックについて説明します。

[廃止されたポート クラス関数](obsolete-port-class-functions.md)

[廃止されたカーネル モード ドライバーのサポート関数](obsolete-kernel-mode-driver-support-functions.md)

 

 





