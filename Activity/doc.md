activity与windowmanagerservice、surfaceflinger怎么关联起来？
activity->session(binder类型，activity中的成员)->windowmanagerservice->windowstate(位于windowmanagerservice对象中)
activity->client(binder类型，activity中的成员)->surfaceflinger->layer(位于surfaceflinger对象中)-(返回)->SurfaceLayer（binder类型）
