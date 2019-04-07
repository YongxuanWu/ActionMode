实验目的
---
    创建上下文操作模式(ActionMode)的上下文菜单
    1、使用ListView或者ListActivity创建 List
    2、为List Item创建ActionMode形式 的上下文菜单 
关键代码
---
```
private String[] names=new String[]{"One","Two","Three","Four","Five"};
    private int[] icons=new int[]{R.mipmap.ic_launcher};
    private ListView listView;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        // 创建一个List集合，List集合的元素是Map
        List<Map<String,Object>> listItems=new ArrayList<>();
        for(int i=0;i<names.length;i++){
            Map<String,Object> listItem=new HashMap<>();
            listItem.put("icon",icons[0]);
            listItem.put("name",names[i]);
            listItems.add(listItem);
        }
        // 创建一个SimpleAdapter
        SimpleAdapter simpleAdapter=new SimpleAdapter(this,listItems,
                                    R.layout.simple_item,
                                    new String[]{"icon","name"},
                                    new int[]{R.id.icon,R.id.name});
        listView=findViewById(R.id.mylist);
        listView.setAdapter(simpleAdapter);
        listView.setChoiceMode(ListView.CHOICE_MODE_MULTIPLE_MODAL);
        listView.setMultiChoiceModeListener(new AbsListView.MultiChoiceModeListener() {
            @Override
            public void onItemCheckedStateChanged(ActionMode mode, int position, long id, boolean checked) {
                    listView.getCheckedItemCount();
                    findViewById(R.id.menu_delete);
            }

            @Override
            public boolean onCreateActionMode(ActionMode mode, Menu menu) {
                MenuInflater inflater = mode.getMenuInflater();
                inflater.inflate(R.menu.menu_delete, menu);
                return true;
            }

            @Override
            public boolean onPrepareActionMode(ActionMode mode, Menu menu) {
                return false;
            }

            @Override
            public boolean onActionItemClicked(ActionMode mode, MenuItem item) {
                switch (item.getItemId()) {
                    case R.id.menu_delete:
                        //deleteSelectedItems();
                        mode.finish(); // Action picked, so close the CAB
                        return true;
                    default:
                        return false;
                }
            }

            @Override
            public void onDestroyActionMode(ActionMode mode) {

            }
        });
    }
```
结果截图
---
![image](https://github.com/YongxuanWu/ActionMode/blob/master/images/p1.jpg)
![image](https://github.com/YongxuanWu/ActionMode/blob/master/images/p2.jpg)
