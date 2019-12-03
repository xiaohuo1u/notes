# notes
work summary
1、isNull 和 isEmpty 的区别：假如一个容器，isnull是用来判断有没有这个容器，而isEmpty是有这个容器，来判断这个容器中的内容有没有东西是不是空的！
2、mysql中不等于会过滤掉null的问题
3、提交代码时使用git忘记push
4、XXXDaoImpl中sql.append()中是类名而非表名
5、分清表字段名和类字段名
6、Git提交代码忘记去掉配置类文件
7、在类中抽取私有方法：
    导出功能中 searchXXX 和 download 方法公用一段代码，可将该段代码抽取成一个私有方法，供其他两个方法使用
    例如：

     private List<FmBankAccountDetailVo> get (FmBankStaticVo vo){//查询所有公司信息
        List<String> classifyList = new ArrayList<String>();
        classifyList.add("LJS");
        classifyList.add("CJS");
        classifyList.add("QJS");
        classifyList.add("LGJ");
        classifyList.add("PH");
        List<PrincipleInfoDto> principleInfoDtoList = queryPrincipleInfoListByClassifyCode(classifyList);
        ...
        ...

        List<FmBankAccountDetailVo> fmFinalDetailVoList = new ArrayList<FmBankAccountDetailVo>();

        ...
         if (StringUtils.isNotBlank(equityStructureOwnStr)) {
            logger.info("开始过滤股权架构所属之前...fmFourthDetailVoList:{}", JSONArray.fromObject(fmFourthDetailVoList));
            List<String> equityStructureOwns = Arrays.asList(equityStructureOwnStr.split(","));
            for (FmBankAccountDetailVo fmBankAccountDetailVo : fmFourthDetailVoList) {
                if (equityStructureOwns.contains(fmBankAccountDetailVo.getEquityStructureOwn())) {
                    fmFinalDetailVoList.add(fmBankAccountDetailVo);
                }
            }
            logger.info("最终过滤集合...fmFinalDetailVoList:{}", JSONArray.fromObject(fmFinalDetailVoList));
        }
        return fmFinalDetailVoList;
     }



      public String searchLuCashBankAccountSource(ModelMap modelMap, Page page,
                                                HttpServletRequest request, FmBankStaticVo vo) {
        //查询所有公司信息
        List<String> classifyList = new ArrayList<String>();
        classifyList.add("LJS");
        classifyList.add("CJS");
        classifyList.add("QJS");
        classifyList.add("LGJ");
        classifyList.add("PH");
        List<PrincipleInfoDto> principleInfoDtoList = queryPrincipleInfoListByClassifyCode(classifyList);
        ...
        ...

        if (StringUtils.isNotBlank(equityStructureOwnStr)) {
            logger.info("开始过滤股权架构所属之前...fmFourthDetailVoList:{}", JSONArray.fromObject(fmFourthDetailVoList));
            List<String> equityStructureOwns = Arrays.asList(equityStructureOwnStr.split(","));
            for (FmBankAccountDetailVo fmBankAccountDetailVo : fmFourthDetailVoList) {
                if (equityStructureOwns.contains(fmBankAccountDetailVo.getEquityStructureOwn())) {
                    fmFinalDetailVoList.add(fmBankAccountDetailVo);
                }
            }
            logger.info("最终过滤集合...fmFinalDetailVoList:{}", JSONArray.fromObject(fmFinalDetailVoList));
        }
        modelMap.put("fmFinalDetailVoList", fmFinalDetailVoList);
        return "/luCashAccount/searchFmBankAccount";
    }
    }
    



    public void download(ModelMap modelMap,
                           FmBankStaticVo vo, Page page,
                           HttpServletRequest request, HttpServletResponse response) {

                               ...

                           List<FmBankAccountDetailVo> fmFinalDetailVoList = get(vo);

                                ...

