---
title: 複数バイナリ オプトイン POOL_NX_OPTIN_AUTO
description: ハードウェア ベンダーが Windows のバージョンごとに別のドライバー バイナリを提供している場合は、POOL_NX_OPTIN_AUTO オプトイン メカニズムを使用することができます。
ms.assetid: 5E6759E3-3AF8-4427-BDD0-DB64B3D480A1
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 35bfdd62da933142cabb4fe4e05f60074be83887
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380290"
---
# <a name="multiple-binary-opt-in-poolnxoptinauto"></a>複数バイナリ オプトイン: プール\_NX\_OPTIN\_自動


ハードウェア ベンダーが Windows のバージョンごとに別のドライバー バイナリを提供している場合は、プールを使用することができます\_NX\_OPTIN\_自動オプトイン メカニズム。 この移植の補助は、Windows 8 以降、ドライバーがサポートする Windows の以前のバージョンごとに個別のドライバー バイナリをビルドします。

をこのオプトイン メカニズムを使用するには、プールを定義\_NX\_OPTIN\_自動 1 = すべてのソース ファイルにオプトインします。 これを行うには、ドライバー プロジェクトの適切なプロパティ ページで次のプリプロセッサの定義を含めます。

`C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN_AUTO=1`

ほとんどのドライバーのこの定義は選択メカニズムをサポートしている Windows のバージョンごとに異なるバイナリの作成を有効にするための十分です。

## <a name="implementation-details"></a>実装の詳細


プール\_NX\_OPTIN\_自動定義を再定義、 **NonPagedPool**定数名に**NonPagedPoolNx**します。 再定義されたプールの種類は、引き続きコンパイル時定数です。 インスタンスに変換するマクロ、 **NonPagedPool**定数名に**NonPagedPoolNx**のインスタンスの変換も行います**NonPagedPoolCacheAligned** に**NonPagedPoolNxCacheAligned します。**

 

 




