## 涉及的表
- gp_users fund_periods 暂时未使用

- fund_trust_oa  基金托管机构   
	1. 删除字段 fund_periods 
	2. 新增字段 fund_id  
	3. 修改接口 oamanagement/add_fund_trust_oa  
	4. 修改接口 oamanagement/edit_fund_trust_oa
	5. 客户端沟通，获取机构信息的业务是否需要返回基金信息

gp_investments GP 跟投  
	1. 删除字段 fund_name fund_periods fund_manage_name 
	2. 修改新增编辑接口删除对应字段新增编辑
	3. 查询接口关联查询返回对应接口数据

gp_manage_fee GP 管理费
	1. 删除字段 fund_name fund_periods fund_manage_name 
	2. 修改新增编辑接口删除对应字段新增编辑
	3. 查询接口关联查询返回对应接口数据

gp_performance_compensation GP 业绩报告
	1. 删除字段 fund_name fund_periods fund_manage_name 
	2. 修改新增编辑接口删除对应字段新增编辑

gp_trans_files GP 交易文件   #TODO
	1. 删除字段 fund_periods 
	2. 新增字段 fund_id  
	3. 修改接口 oamanagement/add_fund_trust_oa  
	4. 修改接口 oamanagement/edit_fund_trust_oa
	5. 客户端沟通，获取机构信息的业务是否需要返回基金信息
	6. upload_gp_user_name 字段有值 upload_go_user_id 字段没值

lp_sub_agreements 
	1. 删除字段 fund_periods 
	2. 新增字段 fund_id  
	3. 修改接口 oamanagement/add_fund_trust_oa  
	4. 修改接口 oamanagement/edit_fund_trust_oa
	5. 客户端沟通，获取机构信息的业务是否需要返回基金信息

performance_agreements 业绩约定
	1. 删除字段 fund_name fund_periods fund_manage_name 
	2. 修改新增编辑接口删除对应字段新增编辑

funds
	1. 删除字段 fund_periods 


// 需求疑问点
1. GP 管理员和 LP 管理员与登陆用户是否有关系
2. gp_account_id lp_account_id 字段关联的是 gp_users lp_users 的主键 
	1. 问题字段，gp_users lp_users 里有个字段叫  account_id
	2. todo 统计哪些表使用了 gp_account_id lp_account_id