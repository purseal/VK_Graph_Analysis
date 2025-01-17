# VK_Graph_Analysis
Инструмент для кластеризации и выделения значимых участников социального графа, построенном на основе групп «‎ВКонтакте»‎
## Описание методов
### get_couples_by_group_ids(access_token, group_ids)
Выгрузка с API ВК множетсва id участников и всех их друзей заданных групп ВК, а также списка пар друзей из этого множетсва. 

Входные данные: 
* access_token - токен доступа с помощью API ВК; 
* group_ids - список id групп ВК, на основе участников которой заполняется список пар друзей.

Выходные данные: 
* список ids, содержащий все уникальные id пользователей ВК, которые есть среди участников групп в списке groups_ids и их друзей; 
* множество пар друзей couples, которое содержит все пары друзей людей из ids; 
* словарь ids_dict, предназначенный для мэппинга id пользователей ВК.
### create_grt_graph(access_token, \*group_ids)
Выгрузка с API ВК множетсва id участников и всех их друзей заданных групп ВК, списка пар друзей из этого множетсва, а также формирование графа на основе id пользователей  которые имеют более одной связи с участниками этих групп.

Входные данные: 
* access_token - токен доступа с помощью API ВК; 
* \*group_ids список id групп ВК.

Выходные данные: 
* объект класса graph_tool.Graph.
### ig_clustering(g, method, method_name)
Кластеризация графа graph_tool.Graph заданным методом кластеризации из библиотеки igraph.

Входные данные:
* g - объект класса graph_tool.Graph;
* method - метод класса igraph.Graph;
* method_name - название метода кластеризации.

Выходные данные:
* объект класса graph_tool.Graph, в котором полученные метки кластеров записаны в свойствах property этого графа, при этом название свойства - method_name.
### clusters_to_graph(g, cluster_prop_name)
Этот метод создаёт на основе графа g граф, количество вершин которого соответствует количеству кластеров cluster_prop_name графа g, размер вершин пропорционален количеству вершин графа g в кластере, а ширина связей - количеству связей между  соответствующими кластерами.

Входные данные:
* g - объект класса graph_tool.Graph;
* cluster_prop_name - название свойства property графа g, содержащего метки кластеров для каждой вершины графа.

Выходные данные:
* объект класса graph_tool.Graph.
### cluster_separation(g, cluster_prop_name)
Удаление рёбер между кластерами графа.

Входные данные: 
* g - объект класса graph_tool.Graph;
* cluster_prop_name - название свойства property графа g, содержащего метки кластеров для каждой вершины графа.

Выходные данные:
* объект класса graph_tool.Graph, в котором удалены все рёбра между кластерами.
