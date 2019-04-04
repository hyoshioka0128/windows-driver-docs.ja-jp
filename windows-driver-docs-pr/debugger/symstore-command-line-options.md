---
title: SymStore のコマンドライン オプション
description: SymStore トランザクションでは、次の構文はサポートされます。 いつでも、最初のパラメーターを追加する必要がありますまたは del します。その他のパラメーターの順序は、素材ではありません。
ms.assetid: 44009878-8f8a-4301-b075-eb0164b4f3a3
keywords:
- SymStore コマンド ライン オプションの Windows デバッグ
ms.date: 03/12/2019
topic_type:
- apiref
api_name:
- SymStore Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eb14a734528f9798126eecabe898fe63a3617240
ms.sourcegitcommit: 71938460f3d04caa4b4d6d0cee695db887ee35e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "57909207"
---
# <a name="symstore-command-line-options"></a>SymStore のコマンドライン オプション

SymStore トランザクションでは、次の構文はサポートされます。 最初のパラメーターは**追加**、**クエリ**または**del**します。使用 **/でしょうか。** 使用可能なオプションを表示します。 

```dbgcmd
symstore add [/r] [/p [/l] [-:MSG Message] [-:REL] [-:NOREFS]] /f File /s Store /t Product [/v Version] [/o] [/c Comment] [/d LogFile] [/compress]

symstore add [/r] [/p [/l] [-:REL] [-:NOREFS]] /g Share /f File /x IndexFile [/a] [/o] [/d LogFile] 

symstore add /y IndexFile /g Share /s Store [/p [-:MSG Message] [-:REL] [-:NOREFS]] /t Product [/v Version] [/o] [/c Comment] [/d LogFile] [/compress]

symstore query [/r] /f File /s Store [/o] [/d LogFile]

symstore del /i ID /s Store [/o] [/d LogFile] 

symstore /? 
```

## <a name="span-idddksymstorecommandlineoptionsdbgspanspan-idddksymstorecommandlineoptionsdbgspanparameters"></a><span id="ddk_symstore_command_line_options_dbg"></span><span id="DDK_SYMSTORE_COMMAND_LINE_OPTIONS_DBG"></span>パラメーター


<span id="________f_______File______"></span><span id="________f_______file______"></span><span id="________F_______FILE______"></span> **/f** *ファイル*   
追加するファイルまたはディレクトリのネットワーク パスを指定します。

<span id="________g_______Share______"></span><span id="________g_______share______"></span><span id="________G_______SHARE______"></span> **/g** *共有*   
サーバーとシンボル ファイルが格納されていた共有を指定します。 使用すると **/f**、*共有*の先頭と一致させるように、*ファイル*指定子。 使用すると **/y**、*共有*元のシンボル ファイル (インデックス ファイルではなく) の場所を指定する必要があります。 これにより後で変更するファイルのパスのこの部分に別のサーバーまたは共有シンボル ファイルを移動する場合にできます。

<span id="________s_______Store______"></span><span id="________s_______store______"></span><span id="________S_______STORE______"></span> **/s** *ストア*   
シンボル ストアのルート ディレクトリを指定します。

<span id="________m_______Prefix______"></span><span id="________m_______prefix______"></span><span id="________M_______PREFIX______"></span> **/m** *プレフィックス*   
SymStore で始まるパスからシンボルを使用すると、*プレフィックス*ファイルを保存する場合や、ポインターを更新します。 このオプションでは使用できません、 **/x**オプション。

<span id="________h___PUB___PRI__"></span><span id="________h___pub___pri__"></span><span id="________H___PUB___PRI__"></span> **/h** { **PUB |PRI** }  
格納またはシンボルを更新するときに (PRI が指定された) 場合、パブリック シンボル (PUB が指定された) 場合、またはプライベート シンボルの使用を好む SymStore をによりします。 このオプションは、バイナリ ファイルへの影響を与えません。

<span id="________i_______ID______"></span><span id="________i_______id______"></span><span id="________I_______ID______"></span> **/i** *ID*   
トランザクションの ID 文字列を指定します。

<span id="________p______"></span><span id="________P______"></span> **/p**   
ファイル自体ではなく、ファイルへのポインターを格納する SymStore をによりします。

<span id="________l______"></span><span id="________L______"></span> **/l**   
指定されたファイルは、*ファイル*ネットワーク パスではなく、ローカル ディレクトリにします。 (このオプションはのみにする場合に使用両方 **/f**と **/p**使用されます)。

<span id="_______-_MSG________Message______"></span><span id="_______-_msg________message______"></span><span id="_______-_MSG________MESSAGE______"></span> **-: MSG** *メッセージ*   
指定した追加*メッセージ*の各ファイルにします。 (このオプションはのみにするときに使用 **/p**使用されます)。

<span id="_______-_REL______"></span><span id="_______-_rel______"></span> **-:REL**   
パスは相対ファイル ポインターことができます。 このオプションの意味、/**l**オプション。 (このオプションはのみにするときに使用 **/p**使用されます)。

<span id="_______-_NOREFS______"></span><span id="_______-_norefs______"></span> **-:NOREFS**   
ファイルおよび格納されているポインターの参照ポインターのファイルの作成を省略します。 このオプションは、変更されているストアは、このオプションを使用して作成されている場合、シンボル ストアの初期作成時にのみ有効です。

<span id="________r______"></span><span id="________R______"></span> **/r**   
ファイルまたはディレクトリの再帰的に追加する SymStore をによりします。

<span id="________t_______Product______"></span><span id="________t_______product______"></span><span id="________T_______PRODUCT______"></span> **/t** *製品*   
製品の名前を指定します。

<span id="________v_______Version______"></span><span id="________v_______version______"></span><span id="________V_______VERSION______"></span> **/v** *バージョン*   
製品のバージョンを指定します。

<span id="________c_______Comment______"></span><span id="________c_______comment______"></span><span id="________C_______COMMENT______"></span> **/c** *コメント*   
トランザクションのコメントを指定します。

<span id="________d_______LogFile______"></span><span id="________d_______logfile______"></span><span id="________D_______LOGFILE______"></span> **/d** *LogFile*   
コマンドの出力に使用するログ ファイルを指定します。 トランザクション情報とその他の出力に送信は、これが含まれていない場合**stdout**します。

<span id="________o______"></span><span id="________O______"></span> **/o**   
詳細な出力を表示する SymStore をによりします。

<span id="________x_______IndexFile______"></span><span id="________x_______indexfile______"></span><span id="________X_______INDEXFILE______"></span> **/x** *IndexFile*   
実際のシンボル ファイルを格納しないように SymStore をによりします。 SymStore が情報を記録する代わりに、 *IndexFile* SymStore シンボル ファイルには後でアクセスを有効になります。

<span id="________a______"></span><span id="________A______"></span> **/a**   
既存のインデックス ファイルに新しいインデックス情報を追加する SymStore をによりします。 (このオプションでのみ使用、 **/x**オプション)。

<span id="________y_______IndexFile______"></span><span id="________y_______indexfile______"></span><span id="________Y_______INDEXFILE______"></span> **/y** *IndexFile*   
SymStore で作成したファイルからデータを読み取ると、 **/x**します。

<span id="________yi_______IndexFile______"></span><span id="________yi_______indexfile______"></span><span id="________YI_______INDEXFILE______"></span> **/yi** *IndexFile*   
トランザクション ID 付きのコメントを追加で作成されたインデックス ファイルの末尾に、/**x**オプション。

<span id="________z___PUB___PRI__"></span><span id="________z___pub___pri__"></span><span id="________Z___PUB___PRI__"></span> **/z** { **PUB |PRI** }  
インデックスの指定されたシンボルの種類のみを SymStore をによりします。 場合**PUB**が指定されている場合、完全なソース情報が削除されているシンボルのみインデックスが作成されます。 場合**PRI**が指定されている場合、完全なソース情報が含まれているシンボルのみインデックスが作成されます。 SymStore はバイナリのシンボルに常にインデックスを作成します。

<span id="________compress______"></span><span id="________COMPRESS______"></span> **/compress**   
SymStore、圧縮されていないファイルのコピーを使用する代わりに、シンボル ストアにコピーする各ファイルの圧縮バージョンを作成するとします。 このオプションは、ファイルといないポインターを格納する場合にのみ有効ですし、その結果、ときに使用することはできません、 **/p**オプションを使用します。

<span id="_______________"></span> **/?**   
SymStore コマンドのヘルプを表示します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

SymStore の詳細については、[シンボル サーバーを使用して、シンボル ストア](symbol-stores-and-symbol-servers.md)を参照してください。









