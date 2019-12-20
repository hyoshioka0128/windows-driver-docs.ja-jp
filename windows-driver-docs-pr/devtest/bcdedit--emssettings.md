---
title: BCDEdit /emssettings
description: /Emssettings オプションは、コンピューターのグローバル緊急管理サービス (EMS) 設定を設定します。 EMS を有効または無効にするには、/ems オプションを使用します。 /Emssettings オプションでは、ブートエントリの EMS を有効または無効にすることはできません。
ms.assetid: 010e852d-ff97-4280-b35b-f1881e249e42
ms.date: 07/03/2018
keywords:
- BCDEdit/emssettings ドライバー開発ツール
topic_type:
- apiref
api_name:
- BCDEdit /emssettings
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5a3809bd9ae6c129ab8654a1d29144d11ba593c8
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209486"
---
# <a name="bcdedit-emssettings"></a>BCDEdit /emssettings


**/Emssettings**オプションは、コンピューターのグローバル緊急管理サービス (EMS) 設定を設定します。 EMS を有効または無効にするには、 **/ems**オプションを使用します。 **/Emssettings**オプションでは、ブートエントリの EMS を有効または無効にすることはできません。

構文 

```
    bcdedit /emssettings [ BIOS ] | [ EMSPORT: port | [EMSBAUDRATE: baudrate] ] 
```

<a name="parameters"></a>パラメーター
----------

**BIOS**   
システムが EMS 構成に BIOS 設定を使用することを指定します。 これは、BIOS で EMS サポートが提供されているシステムでのみ機能します。

 **Emsport:** *ポート*   
EMS ポートとして使用するシリアルポートを指定します。 このパラメーターを**BIOS**オプションと共に指定することはできません。

**Emsbaudrate レート:** *ボーレート*   
EMS に使用するシリアルボーレートを指定します。 このコマンドを BIOS で指定することはできません。 *ボーレート*は省略可能で、既定値は 9600 bps です。

### <a name="comments"></a>コメント

Windows のインストール後に EMS コンソールのリダイレクトを正しく有効にするには、コンピューターが帯域外通信に使用するポートと転送速度を認識している必要があります。 Windows では、これらの同じ設定を EMS コンソールのリダイレクトに使用します。

BIOS ファームウェアが搭載されたコンピューターと ACPI シリアルポートコンソールのリダイレクト (SPCR) テーブルでは、Windows は、SPCR テーブルのエントリを読み取って、BIOS で設定された帯域外設定を見つけることができます。 これらのシステムでは、 **BIOS**パラメーターを使用して、Windows に対してポートの設定を SPCR テーブルで探すように指示することも、 **emsport:**<em>port</em>パラメーターと**emsボーレート:**<em>ボーレート</em>パラメーターを使用して、spcr テーブルの設定を上書きすることもできます。

BIOS ファームウェアを搭載していても、SPCR テーブルがないコンピューターでは、BCDEdit を使用し、 **emスポーツ:**<em>port</em>パラメーターを指定した **/emssettings**コマンドを使用してポートを指定し、 **emsボーレート:**<em>ボー</em>レートパラメーターを使用して伝送速度を指定します。

すべてのシステムで、 [**BCDEdit/ems**](bcdedit--ems.md)コマンドを使用し、ブートエントリを指定して、ブートエントリが読み込まれるオペレーティングシステムで ems コンソールのリダイレクトを有効にします。

このセクションで説明するブートパラメーターを使用すると、Windows のインストール後に EMS コンソールのリダイレクトが有効になります。 

詳細な例については、「[ブートパラメーターを使用した EMS リダイレクトの有効化](https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-parameters-to-enable-ems-redirection)」を参照してください。

 

 





